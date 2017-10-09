---
title: 'Connect Arduino (C) tooAzure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Adafruit Doezelaar M0 Wi-Fi- en monitors binnenkomende berichten uit uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooAdafruit Doezelaar M0 Wi-Fi uit uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: arduino besturingselement geleid vanaf web arduino besturingselement geleid via het web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="35bde-105">Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="35bde-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="35bde-106">In dit artikel kunt u een voorbeeld van toepassing op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino implementeren.</span><span class="sxs-lookup"><span data-stu-id="35bde-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="35bde-107">Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="35bde-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="35bde-108">U ook uitvoeren een gulp taak op uw computer toosend berichten tooyour Arduino mededelingenbord van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="35bde-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="35bde-109">Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="35bde-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="35bde-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="35bde-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="35bde-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="35bde-111">What you will do</span></span>
* <span data-ttu-id="35bde-112">Sluit Hallo voorbeeld toepassing tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="35bde-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="35bde-113">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="35bde-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="35bde-114">Berichten verzenden van uw IoT hub tooyour Arduino mededelingenbord tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="35bde-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="35bde-115">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="35bde-115">What you will learn</span></span>
<span data-ttu-id="35bde-116">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="35bde-116">In this article, you will learn:</span></span>
* <span data-ttu-id="35bde-117">Hoe toomonitor binnenkomende berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="35bde-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="35bde-118">Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooyour Arduino het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="35bde-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="35bde-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="35bde-119">What you need</span></span>
* <span data-ttu-id="35bde-120">Het mededelingenbord Arduino instellen voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="35bde-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="35bde-121">hoe tooset van het mededelingenbord Arduino zien toolearn [configureren van uw apparaat][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="35bde-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="35bde-122">Een IoT-hub die wordt gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="35bde-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="35bde-123">toolearn hoe toocreate uw IoT-hub Zie [maken van uw Azure-IoT-Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="35bde-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="35bde-124">Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="35bde-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="35bde-125">Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="35bde-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="35bde-126">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="35bde-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="35bde-127">Kennisgeving Hallo `app.ino` bestand in Hallo `app` submap.</span><span class="sxs-lookup"><span data-stu-id="35bde-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="35bde-128">Hallo `app.ino` bestand is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="35bde-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="35bde-129">Hallo `blinkLED` functie Hallo LED knippert.</span><span class="sxs-lookup"><span data-stu-id="35bde-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing][repo-structure]

2. <span data-ttu-id="35bde-131">Seriële poort Hallo Hallo-apparaat met Hallo apparaat detectie cli verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="35bde-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="35bde-132">U moet een uitvoer die vergelijkbaar toohello volgende wordt weergegeven en Hallo usb COM-poort voor het mededelingenbord Arduino vinden:</span><span class="sxs-lookup"><span data-stu-id="35bde-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Detectie van netwerkapparaten][device-discovery]

3. <span data-ttu-id="35bde-134">Open Hallo bestand `config.json` in Hallo les map en de waarde van de invoer Hallo Hallo COM-poortnummer gevonden:</span><span class="sxs-lookup"><span data-stu-id="35bde-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="35bde-136">Voor Hallo COM-poort op Windows-platform, heeft het Hallo-indeling van `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="35bde-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="35bde-137">Op Mac OS of Ubuntu wordt gestart met `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="35bde-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="35bde-138">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="35bde-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="35bde-139">Zorg Hallo vervangingen in Hallo na `config-arduino.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="35bde-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="35bde-140">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt Hallo stap toohello taak voor het implementeren van overslaan en Hallo-voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35bde-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="35bde-141">Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-arduino.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="35bde-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="35bde-142">Hallo `config-arduino.json` bestand bevindt zich in de submap Hallo van de basismap.</span><span class="sxs-lookup"><span data-stu-id="35bde-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Inhoud van Hallo config arduino.json bestand][config-arduino-json]

   * <span data-ttu-id="35bde-144">Vervang **[Wi-Fi-SSID]** met uw Wi-Fi-SSID die toohello Internet verbonden.</span><span class="sxs-lookup"><span data-stu-id="35bde-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="35bde-145">Vervang **[Wi-Fi-wachtwoord]** met het Wi-Fi-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="35bde-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="35bde-146">Hallo tekenreeks verwijderen als uw Wi-Fi geen wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="35bde-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="35bde-147">Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="35bde-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="35bde-148">Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name}` opdracht.</span><span class="sxs-lookup"><span data-stu-id="35bde-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="35bde-149">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="35bde-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="35bde-150">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op het mededelingenbord Arduino door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="35bde-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="35bde-151">Hallo gulp opdracht implementeert Hallo voorbeeld toepassing tooyour Arduino mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="35bde-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="35bde-152">Vervolgens het Hallo toepassing uitvoert op het mededelingenbord Arduino en een afzonderlijke taak op de host computer toosend 20 knipperen berichten tooyour Arduino mededelingenbord van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="35bde-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="35bde-153">Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="35bde-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="35bde-154">Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooyour Arduino mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="35bde-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="35bde-155">Voor elk bericht knipperen die Hallo mededelingenbord ontvangt, de voorbeeldtoepassing Hallo Hallo roept `blinkLED` functie tooblink Hallo LED.</span><span class="sxs-lookup"><span data-stu-id="35bde-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="35bde-156">U ziet Hallo LED elke twee seconden knipperen zoals Hallo gulp taak 20 berichten uit uw IoT hub tooyour Arduino mededelingenbord verzendt.</span><span class="sxs-lookup"><span data-stu-id="35bde-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="35bde-157">Hallo laatste is een een 'stop'-bericht dat wordt gestopt Hallo-toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35bde-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen][sample-application]

## <a name="summary"></a><span data-ttu-id="35bde-159">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="35bde-159">Summary</span></span>
<span data-ttu-id="35bde-160">U hebt berichten uit uw IoT hub tooyour Arduino mededelingenbord tooblink Hallo LED verzonden.</span><span class="sxs-lookup"><span data-stu-id="35bde-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="35bde-161">de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.</span><span class="sxs-lookup"><span data-stu-id="35bde-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35bde-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="35bde-162">Next steps</span></span>
<span data-ttu-id="35bde-163">[Hallo in- en uitschakelen gedrag van Hallo LED wijzigen][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="35bde-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md