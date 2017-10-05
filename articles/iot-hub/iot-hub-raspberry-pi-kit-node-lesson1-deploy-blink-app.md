---
featureFlags: usabilla
title: 'Raspberry Pi (knooppunt) verbinden met Azure IoT - les 1: app implementeren | Microsoft Docs'
description: Klonen van de voorbeeldtoepassing Node.js vanuit GitHub en gulp voor het implementeren van deze toepassing op het mededelingenbord frambozen Pi 3. Deze voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Raspberry pi geleid knipperen, knipperen geleid met raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="16f95-105">De Blink-toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="16f95-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="16f95-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="16f95-106">What you will do</span></span>
<span data-ttu-id="16f95-107">Klonen van de voorbeeldtoepassing Node.js vanuit GitHub en het hulpprogramma gulp gebruiken voor het implementeren van de voorbeeldtoepassing op uw frambozen Pi 3.</span><span class="sxs-lookup"><span data-stu-id="16f95-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="16f95-108">De voorbeeldtoepassing knippert de LED verbonden met de kaart elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="16f95-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="16f95-109">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="16f95-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="16f95-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="16f95-110">What you will learn</span></span>
<span data-ttu-id="16f95-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="16f95-111">In this article, you will learn:</span></span>

* <span data-ttu-id="16f95-112">Het gebruik van de `device-discover-cli` hulpprogramma netwerken informatie ophalen over Pi.</span><span class="sxs-lookup"><span data-stu-id="16f95-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="16f95-113">Informatie over het implementeren en uitvoeren van de voorbeeldtoepassing op Pi.</span><span class="sxs-lookup"><span data-stu-id="16f95-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="16f95-114">Het implementeren en foutopsporing op afstand worden uitgevoerd op Pi-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="16f95-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="16f95-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="16f95-115">What you need</span></span>
<span data-ttu-id="16f95-116">U moet hebt voltooid de volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="16f95-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="16f95-117">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="16f95-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="16f95-118">Download de hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="16f95-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="16f95-119">Het IP-adres en hostnaam de naam van Pi verkrijgen</span><span class="sxs-lookup"><span data-stu-id="16f95-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="16f95-120">Open een opdrachtprompt in Windows of in een terminal in Mac OS of Ubuntu en voer vervolgens de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="16f95-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="16f95-121">Hier ziet u uitvoer die vergelijkbaar is met het volgende:</span><span class="sxs-lookup"><span data-stu-id="16f95-121">You should see an output that is similar to the following:</span></span>

![Detectie van netwerkapparaten](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="16f95-123">Noteer de `IP address` en `hostname` van Pi.</span><span class="sxs-lookup"><span data-stu-id="16f95-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="16f95-124">U moet deze informatie later in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="16f95-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="16f95-125">Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="16f95-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="16f95-126">Bijvoorbeeld, als uw computer is verbonden met een draadloos netwerk als Pi is verbonden met een bekabeld netwerk, ziet u mogelijk niet het IP-adres in de uitvoer devdisco.</span><span class="sxs-lookup"><span data-stu-id="16f95-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="16f95-127">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="16f95-127">Clone the sample application</span></span>
<span data-ttu-id="16f95-128">U opent de voorbeeldcode door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="16f95-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="16f95-129">Kloon de opslagplaats voorbeeld vanuit GitHub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="16f95-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="16f95-130">De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="16f95-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="16f95-132">De `app.js` bestand de `app` submap is het belangrijkste bronbestand dat de code voor het besturingselement de LED bevat.</span><span class="sxs-lookup"><span data-stu-id="16f95-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="16f95-133">Afhankelijkheden voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="16f95-133">Install application dependencies</span></span>
<span data-ttu-id="16f95-134">Installeer de bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing met de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="16f95-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="16f95-135">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="16f95-135">Configure the device connection</span></span>
<span data-ttu-id="16f95-136">Volg deze stappen voor het configureren van de apparaatverbinding:</span><span class="sxs-lookup"><span data-stu-id="16f95-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="16f95-137">Het configuratiebestand van het apparaat genereren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="16f95-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="16f95-138">Het configuratiebestand `config-raspberrypi.json` bevat de referenties van de gebruiker die u gebruikt voor aanmelding bij Pi.</span><span class="sxs-lookup"><span data-stu-id="16f95-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="16f95-139">Om te voorkomen dat het lek van gebruikersreferenties, het configuratiebestand wordt gegenereerd in de submap `.iot-hub-getting-started` van de basismap op uw computer.</span><span class="sxs-lookup"><span data-stu-id="16f95-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="16f95-140">Open het configuratiebestand van het apparaat in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="16f95-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="16f95-141">Vervang de tijdelijke aanduiding `[device hostname or IP address]` met het IP-adres of de hostnaam die u eerder hebt verkregen in ' de IP-adres en hostnaam naam achterhalen van Pi."</span><span class="sxs-lookup"><span data-stu-id="16f95-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="16f95-143">U kunt SSH-sleutel in plaats van de gebruikersnaam en wachtwoord gebruiken bij het verbinden met frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="16f95-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="16f95-144">Hiervoor hebt, moet u de sleutel genereren met **ssh-keygen** en **ssh-exemplaar-id pi @\<adres van apparaat\>**.</span><span class="sxs-lookup"><span data-stu-id="16f95-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="16f95-145">In Windows deze opdrachten zijn beschikbaar in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="16f95-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="16f95-146">Op Mac OS die u wilt uitvoeren **brew installeren ssh-exemplaar-id**.</span><span class="sxs-lookup"><span data-stu-id="16f95-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="16f95-147">Na het uploaden is de sleutel tot het Pi frambozen, Vervang **device_password** met **device_key_path** eigenschap in **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="16f95-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="16f95-148">Bijgewerkte regels ziet er als hieronder:</span><span class="sxs-lookup"><span data-stu-id="16f95-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="16f95-149">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="16f95-149">Congratulations!</span></span> <span data-ttu-id="16f95-150">U hebt de eerste voorbeeldtoepassing voor Pi gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16f95-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="16f95-151">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="16f95-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="16f95-152">Node.js en NPM op Pi installeren</span><span class="sxs-lookup"><span data-stu-id="16f95-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="16f95-153">Node.js en NPM met Pi installeren met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="16f95-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="16f95-154">Deze taak duurt 10 minuten de eerste keer dat u deze uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16f95-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="16f95-155">Implementeren en uitvoeren van de voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="16f95-155">Deploy and run the sample app</span></span>
<span data-ttu-id="16f95-156">Implementeren en uitvoeren van de voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="16f95-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="16f95-157">Controleer of de app werkt</span><span class="sxs-lookup"><span data-stu-id="16f95-157">Verify the app works</span></span>
<span data-ttu-id="16f95-158">U ziet nu de LED op Pi knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="16f95-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="16f95-159">Als u niet de LED knippert ziet, raadpleegt u de [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor oplossingen voor bekende problemen.</span><span class="sxs-lookup"><span data-stu-id="16f95-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="16f95-160">![LED knippert](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="16f95-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="16f95-161">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="16f95-161">Summary</span></span>
<span data-ttu-id="16f95-162">U hebt de vereiste hulpmiddelen voor het werken met Pi geïnstalleerd en een voorbeeldtoepassing tot Pi de LED knipperen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="16f95-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="16f95-163">U kunt nu maken, implementeren en uitvoeren van een ander voorbeeld van een toepassing die Pi verbindt met Azure IoT Hub berichten te verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="16f95-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16f95-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16f95-164">Next steps</span></span>
[<span data-ttu-id="16f95-165">Download de Azure-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="16f95-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

