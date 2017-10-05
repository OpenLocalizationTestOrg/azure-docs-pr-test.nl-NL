---
title: 'Raspberry Pi (C) verbinden met Azure IoT - les 1: app implementeren | Microsoft Docs'
description: Klonen van de voorbeeldtoepassing C vanuit GitHub en gulp voor het implementeren van deze toepassing op het mededelingenbord frambozen Pi 3. Deze voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Raspberry pi geleid knipperen, knipperen geleid met raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="d4b84-105">De Blink-toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="d4b84-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d4b84-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="d4b84-106">What you will do</span></span>
<span data-ttu-id="d4b84-107">Klonen van de voorbeeldtoepassing C vanuit GitHub en het hulpprogramma gulp gebruiken voor het implementeren van de voorbeeldtoepassing in frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="d4b84-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span></span> <span data-ttu-id="d4b84-108">De voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="d4b84-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="d4b84-109">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d4b84-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d4b84-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="d4b84-110">What you will learn</span></span>
<span data-ttu-id="d4b84-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="d4b84-111">In this article, you will learn:</span></span>

* <span data-ttu-id="d4b84-112">Het gebruik van de `device-discover-cli` hulpprogramma netwerken informatie ophalen over Pi.</span><span class="sxs-lookup"><span data-stu-id="d4b84-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="d4b84-113">Informatie over het implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="d4b84-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="d4b84-114">Het implementeren en foutopsporing op afstand worden uitgevoerd op Pi-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d4b84-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d4b84-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="d4b84-115">What you need</span></span>
<span data-ttu-id="d4b84-116">U moet hebt voltooid de volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="d4b84-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="d4b84-117">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="d4b84-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="d4b84-118">Download de hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="d4b84-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="d4b84-119">Het IP-adres en hostnaam de naam van Pi verkrijgen</span><span class="sxs-lookup"><span data-stu-id="d4b84-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="d4b84-120">Open een opdrachtprompt in Windows of in een terminal in Mac OS of Ubuntu en voer vervolgens de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4b84-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="d4b84-121">Hier ziet u uitvoer die vergelijkbaar is met het volgende:</span><span class="sxs-lookup"><span data-stu-id="d4b84-121">You should see an output that is similar to the following:</span></span>

![Detectie van netwerkapparaten](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="d4b84-123">Noteer de `IP address` en `hostname` van Pi.</span><span class="sxs-lookup"><span data-stu-id="d4b84-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="d4b84-124">U moet deze informatie later in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d4b84-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="d4b84-125">Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="d4b84-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="d4b84-126">Bijvoorbeeld, als uw computer is verbonden met een draadloos netwerk als Pi is verbonden met een bekabeld netwerk, ziet u mogelijk niet het IP-adres in de uitvoer devdisco.</span><span class="sxs-lookup"><span data-stu-id="d4b84-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="d4b84-127">Open de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="d4b84-127">Open the sample application</span></span>
<span data-ttu-id="d4b84-128">U opent de voorbeeldtoepassing door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d4b84-128">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="d4b84-129">Kloon de opslagplaats voorbeeld vanuit GitHub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4b84-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="d4b84-130">De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d4b84-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="d4b84-132">De `main.c` bestand de `app` submap is het belangrijkste bronbestand dat de code voor het besturingselement de LED bevat.</span><span class="sxs-lookup"><span data-stu-id="d4b84-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="d4b84-133">Afhankelijkheden voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="d4b84-133">Install application dependencies</span></span>
<span data-ttu-id="d4b84-134">Installeer de bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing met de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="d4b84-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="d4b84-135">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="d4b84-135">Configure the device connection</span></span>
<span data-ttu-id="d4b84-136">Volg deze stappen voor het configureren van de apparaatverbinding:</span><span class="sxs-lookup"><span data-stu-id="d4b84-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="d4b84-137">Het configuratiebestand van het apparaat genereren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4b84-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="d4b84-138">Het configuratiebestand `config-raspberrypi.json` bevat de referenties van de gebruiker die u gebruikt voor aanmelding bij Pi.</span><span class="sxs-lookup"><span data-stu-id="d4b84-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="d4b84-139">Om te voorkomen dat het lek van gebruikersreferenties, het configuratiebestand wordt gegenereerd in de submap `.iot-hub-getting-started` van de basismap op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d4b84-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="d4b84-140">Open het configuratiebestand van het apparaat in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4b84-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="d4b84-141">Vervang de tijdelijke aanduiding `[device hostname or IP address]` met het IP-adres of de hostnaam die u eerder hebt verkregen in ' de IP-adres en hostnaam naam achterhalen van Pi."</span><span class="sxs-lookup"><span data-stu-id="d4b84-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="d4b84-143">U kunt SSH-sleutel in plaats van de gebruikersnaam en wachtwoord gebruiken bij het verbinden met frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="d4b84-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="d4b84-144">Hiervoor hebt, moet u de sleutel genereren met **ssh-keygen** en **ssh-exemplaar-id pi @\<adres van apparaat\>**.</span><span class="sxs-lookup"><span data-stu-id="d4b84-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="d4b84-145">In Windows deze opdrachten zijn beschikbaar in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="d4b84-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="d4b84-146">Op Mac OS die u wilt uitvoeren **brew installeren ssh-exemplaar-id**.</span><span class="sxs-lookup"><span data-stu-id="d4b84-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="d4b84-147">Na het uploaden is de sleutel tot het Pi frambozen, Vervang **device_password** met **device_key_path** eigenschap in **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="d4b84-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="d4b84-148">Bijgewerkte regels ziet er als hieronder:</span><span class="sxs-lookup"><span data-stu-id="d4b84-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="d4b84-149">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="d4b84-149">Congratulations!</span></span> <span data-ttu-id="d4b84-150">U hebt de eerste voorbeeldtoepassing voor Pi gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4b84-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="d4b84-151">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="d4b84-151">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="d4b84-152">De Azure IoT-Hub SDK op Pi installeren</span><span class="sxs-lookup"><span data-stu-id="d4b84-152">Install the Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="d4b84-153">Azure IoT Hub SDK installeren op Pi met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4b84-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="d4b84-154">Deze taak kan voltooien van de eerste keer dat u het uitvoeren van enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="d4b84-154">This task might take a few minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="d4b84-155">Implementeren en uitvoeren van de voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="d4b84-155">Deploy and run the sample app</span></span>
<span data-ttu-id="d4b84-156">Implementeren en uitvoeren van de voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d4b84-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="d4b84-157">Controleer of de app werkt</span><span class="sxs-lookup"><span data-stu-id="d4b84-157">Verify the app works</span></span>
<span data-ttu-id="d4b84-158">De voorbeeldtoepassing wordt automatisch beëindigd nadat de LED voor 20 keer knippert.</span><span class="sxs-lookup"><span data-stu-id="d4b84-158">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="d4b84-159">Als u niet de LED knippert ziet, raadpleegt u de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-c-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="d4b84-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="d4b84-160">![LED knippert](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="d4b84-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="d4b84-161">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d4b84-161">Summary</span></span>
<span data-ttu-id="d4b84-162">U hebt de vereiste hulpmiddelen voor het werken met Pi geïnstalleerd en een voorbeeldtoepassing tot Pi de LED knipperen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d4b84-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="d4b84-163">U kunt nu maken, implementeren en uitvoeren van een ander voorbeeld van een toepassing die Pi verbindt met Azure IoT Hub berichten te verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4b84-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4b84-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4b84-164">Next steps</span></span>
[<span data-ttu-id="d4b84-165">Azure-hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="d4b84-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

