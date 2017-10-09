---
title: 'Verbinding maken met Arduino tooAzure IoT - les 1: app implementeren | Microsoft Docs'
description: Hallo voorbeeldtoepassing Arduino vanuit GitHub klonen en voer gulp toodeploy deze toepassing tooyour Adafruit Doezelaar M0 Wi-Fi. Deze voorbeeldtoepassing knippert Hallo GPIO
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino geleid projecten, arduino geleid knipperen, arduino geleid knipperen code, arduino knipperen programma, arduino knipperen voorbeeld
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="8bd91-105">Hallo knipperen toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="8bd91-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8bd91-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="8bd91-106">What you will do</span></span>
<span data-ttu-id="8bd91-107">Hallo voorbeeldtoepassing Arduino vanuit GitHub klonen en Hallo gulp hulpprogramma toodeploy Hallo voorbeeld toepassing tooyour Adafruit Doezelaar M0 Wi-Fi Arduino mededelingenbord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8bd91-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="8bd91-108">Hallo voorbeeld toepassing knipperen Hallo GPIO #13 op barod geleid om twee seconden.</span><span class="sxs-lookup"><span data-stu-id="8bd91-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="8bd91-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="8bd91-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8bd91-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="8bd91-110">What you will learn</span></span>
* <span data-ttu-id="8bd91-111">Hoe toodeploy en Voer Hallo voorbeeldtoepassing op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="8bd91-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8bd91-112">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8bd91-112">What you need</span></span>
<span data-ttu-id="8bd91-113">U moet hebben voltooid Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="8bd91-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="8bd91-114">[Uw apparaat configureren][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="8bd91-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="8bd91-115">[Hallo-hulpprogramma's ophalen][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="8bd91-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="8bd91-116">Open Hallo-voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="8bd91-116">Open hello sample application</span></span>
<span data-ttu-id="8bd91-117">tooopen hello voorbeeldtoepassing, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8bd91-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="8bd91-118">Hallo voorbeeld opslagplaats vanuit GitHub door het uitvoeren van de volgende opdracht Hallo klonen:</span><span class="sxs-lookup"><span data-stu-id="8bd91-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="8bd91-119">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="8bd91-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

<span data-ttu-id="8bd91-121">Hallo `app.ino` bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toocontrol Hallo LED bevat.</span><span class="sxs-lookup"><span data-stu-id="8bd91-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="8bd91-122">Afhankelijkheden voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="8bd91-122">Install application dependencies</span></span>
<span data-ttu-id="8bd91-123">Hallo-bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="8bd91-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="8bd91-124">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="8bd91-124">Configure hello device connection</span></span>
<span data-ttu-id="8bd91-125">tooconfigure Hallo apparaatverbinding, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8bd91-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="8bd91-126">Seriële poort Hallo Hallo-apparaat met Hallo apparaat detectie cli verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="8bd91-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="8bd91-127">U moet een uitvoer die vergelijkbaar toohello volgende wordt weergegeven en het vinden van de Hallo usb COM-poort voor deze kaart Arduino: ![detectie van netwerkapparaten][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="8bd91-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="8bd91-128">Open Hallo bestand `config.json` in les map Hallo en toe te voegen waarde Hallo Hallo COM-poortnummer gevonden:</span><span class="sxs-lookup"><span data-stu-id="8bd91-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > <span data-ttu-id="8bd91-130">Voor Hallo COM-poort op Windows-platform, heeft het Hallo-indeling van `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="8bd91-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="8bd91-131">Op Mac OS of Ubuntu en deze begint met `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="8bd91-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="8bd91-132">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="8bd91-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="8bd91-133">Hallo vereist hulpprogramma's voor uw kaart Arduino installeren</span><span class="sxs-lookup"><span data-stu-id="8bd91-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="8bd91-134">Installeer hello Azure IoT Hub SDK voor uw kaart Arduino Hallo na de opdracht uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="8bd91-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="8bd91-135">Deze taak kan duren voordat een toocomplete lange tijd, afhankelijk van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="8bd91-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd91-136">Sluit Hallo Arduino IDE-exemplaar wordt uitgevoerd bij het uitvoeren van taken gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="8bd91-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="8bd91-137">Implementeren en Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8bd91-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="8bd91-138">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="8bd91-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="8bd91-139">Controleer of de app werkt het Hallo</span><span class="sxs-lookup"><span data-stu-id="8bd91-139">Verify hello app works</span></span>
<span data-ttu-id="8bd91-140">Als er geen Hallo LED knippert, raadpleegt u Hallo [probleemoplossingsgids] [ troubleshooting-page] voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="8bd91-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![LED knippert][led-blinking]

## <a name="summary"></a><span data-ttu-id="8bd91-142">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8bd91-142">Summary</span></span>
<span data-ttu-id="8bd91-143">U hebt geïnstalleerd Hallo vereist extra toowork met het mededelingenbord Arduino en een voorbeeld toepassing tooyour Arduino mededelingenbord tooblink Hallo LED geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8bd91-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="8bd91-144">U kunt nu maken, implementeren, en voer een ander voorbeeld van een toepassing die uw Arduino mededelingenbord tooAzure IoT Hub toosend verbinding maakt en berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8bd91-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd91-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bd91-145">Next steps</span></span>
<span data-ttu-id="8bd91-146">[Hello Azure-hulpprogramma's ophalen][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="8bd91-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md