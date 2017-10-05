---
title: 'Arduino verbinden met Azure IoT - les 1: app implementeren | Microsoft Docs'
description: Klonen van de voorbeeldtoepassing Arduino vanuit GitHub, en voer gulp voor het implementeren van deze toepassing naar uw Adafruit Doezelaar M0 Wi-Fi. Deze voorbeeldtoepassing knippert de GPIO
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
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="f8cd1-105">De Blink-toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="f8cd1-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f8cd1-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="f8cd1-106">What you will do</span></span>
<span data-ttu-id="f8cd1-107">Klonen van de voorbeeldtoepassing Arduino vanuit GitHub en het hulpprogramma gulp gebruiken voor het implementeren van de voorbeeldtoepassing op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="f8cd1-108">De voorbeeld-toepassing knipperen de GPIO #13 op barod geleid om twee seconden.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="f8cd1-109">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="f8cd1-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f8cd1-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="f8cd1-110">What you will learn</span></span>
* <span data-ttu-id="f8cd1-111">Informatie over het implementeren en uitvoeren van de voorbeeldtoepassing op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f8cd1-112">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="f8cd1-112">What you need</span></span>
<span data-ttu-id="f8cd1-113">U moet hebt voltooid de volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="f8cd1-114">[Uw apparaat configureren][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="f8cd1-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="f8cd1-115">[Download de hulpprogramma 's][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="f8cd1-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="f8cd1-116">Open de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="f8cd1-116">Open the sample application</span></span>
<span data-ttu-id="f8cd1-117">U opent de voorbeeldtoepassing door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="f8cd1-118">Kloon de opslagplaats voorbeeld vanuit GitHub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="f8cd1-119">De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

<span data-ttu-id="f8cd1-121">De `app.ino` bestand de `app` submap is het belangrijkste bronbestand dat de code voor het besturingselement de LED bevat.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="f8cd1-122">Afhankelijkheden voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="f8cd1-122">Install application dependencies</span></span>
<span data-ttu-id="f8cd1-123">Installeer de bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing met de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="f8cd1-124">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="f8cd1-124">Configure the device connection</span></span>
<span data-ttu-id="f8cd1-125">Volg deze stappen voor het configureren van de apparaatverbinding:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="f8cd1-126">De seriële poort van het apparaat met de apparaat-detectie cli verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="f8cd1-127">U moet een uitvoer die vergelijkbaar is met het volgende weergegeven en de usb-COM-poort vinden voor uw kaart Arduino: ![detectie van netwerkapparaten][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="f8cd1-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="f8cd1-128">Open het bestand `config.json` in de map les en voeg de waarde van de COM-poortnummer gevonden:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > <span data-ttu-id="f8cd1-130">Voor de COM-poort op Windows-platform, heeft de indeling van `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="f8cd1-131">Op Mac OS of Ubuntu en deze begint met `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="f8cd1-132">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="f8cd1-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="f8cd1-133">De vereiste hulpprogramma's voor uw kaart Arduino installeren</span><span class="sxs-lookup"><span data-stu-id="f8cd1-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="f8cd1-134">Installeer de Azure IoT Hub SDK voor uw kaart Arduino met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="f8cd1-135">Deze taak kan lang duren om uit te voeren, afhankelijk van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="f8cd1-136">Sluit de Arduino IDE exemplaar dat wordt uitgevoerd bij het uitvoeren van taken gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="f8cd1-137">Implementeren en uitvoeren van de voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="f8cd1-137">Deploy and run the sample app</span></span>
<span data-ttu-id="f8cd1-138">Implementeren en uitvoeren van de voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f8cd1-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="f8cd1-139">Controleer of de app werkt</span><span class="sxs-lookup"><span data-stu-id="f8cd1-139">Verify the app works</span></span>
<span data-ttu-id="f8cd1-140">Als u niet de LED knippert ziet, raadpleegt u de [probleemoplossingsgids] [ troubleshooting-page] voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![LED knippert][led-blinking]

## <a name="summary"></a><span data-ttu-id="f8cd1-142">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f8cd1-142">Summary</span></span>
<span data-ttu-id="f8cd1-143">U hebt geïnstalleerd, de vereiste hulpmiddelen voor het werken met het mededelingenbord Arduino en een voorbeeld van toepassing op het mededelingenbord Arduino knipperen de LED geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="f8cd1-144">U kunt nu maken, implementeren en uitvoeren van een ander voorbeeld van een toepassing die het mededelingenbord Arduino verbindt met Azure IoT Hub berichten te verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="f8cd1-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8cd1-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8cd1-145">Next steps</span></span>
<span data-ttu-id="f8cd1-146">[Download de Azure-hulpprogramma 's][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="f8cd1-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md