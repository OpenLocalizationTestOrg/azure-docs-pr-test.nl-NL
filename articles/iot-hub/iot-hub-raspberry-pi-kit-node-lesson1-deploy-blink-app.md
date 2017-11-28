---
featureFlags: usabilla
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 1: app implementeren | Microsoft Docs'
description: Kloon Hallo voorbeeldtoepassing Node.js vanuit GitHub en gulp toodeploy het mededelingenbord tooyour frambozen Pi 3 van deze toepassing. Deze voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden.
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
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="bf377-105">Hallo knipperen toepassing maken en implementeren</span><span class="sxs-lookup"><span data-stu-id="bf377-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bf377-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bf377-106">What you will do</span></span>
<span data-ttu-id="bf377-107">Hallo voorbeeldtoepassing Node.js vanuit GitHub klonen en Hallo gulp hulpprogramma toodeploy Hallo voorbeeld toepassing tooyour frambozen Pi 3 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf377-107">Clone hello sample Node.js application from GitHub and use hello gulp tool toodeploy hello sample application tooyour Raspberry Pi 3.</span></span> <span data-ttu-id="bf377-108">Hallo-voorbeeldtoepassing knippert Hallo LED verbonden toohello mededelingenbord elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="bf377-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="bf377-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bf377-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bf377-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bf377-110">What you will learn</span></span>
<span data-ttu-id="bf377-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="bf377-111">In this article, you will learn:</span></span>

* <span data-ttu-id="bf377-112">Hoe toouse hello `device-discover-cli` hulpprogramma tooretrieve informatie over Pi over het netwerk.</span><span class="sxs-lookup"><span data-stu-id="bf377-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="bf377-113">Hoe toodeploy en Voer Hallo voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="bf377-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="bf377-114">Hoe toodeploy en foutopsporing toepassingen die worden uitgevoerd op afstand met Pi.</span><span class="sxs-lookup"><span data-stu-id="bf377-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bf377-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bf377-115">What you need</span></span>
<span data-ttu-id="bf377-116">U moet hebben voltooid Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="bf377-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="bf377-117">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="bf377-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="bf377-118">Hallo-hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="bf377-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="bf377-119">Hallo IP-adres en hostnaam naam verkregen van Pi</span><span class="sxs-lookup"><span data-stu-id="bf377-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="bf377-120">Open een opdrachtprompt in Windows of in een terminal in Mac OS of Ubuntu en voer vervolgens Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bf377-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="bf377-121">Hier ziet u uitvoer die vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="bf377-121">You should see an output that is similar toohello following:</span></span>

![Detectie van netwerkapparaten](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="bf377-123">Let op Hallo `IP address` en `hostname` van Pi.</span><span class="sxs-lookup"><span data-stu-id="bf377-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="bf377-124">U moet deze informatie later in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="bf377-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="bf377-125">Zorg ervoor dat Pi verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="bf377-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="bf377-126">Bijvoorbeeld, als uw computer verbonden tooa draadloze netwerk is wanneer Pi verbonden tooa standaardnetwerk is, ziet u mogelijk niet Hallo IP-adres in Hallo devdisco uitvoer.</span><span class="sxs-lookup"><span data-stu-id="bf377-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="bf377-127">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="bf377-127">Clone hello sample application</span></span>
<span data-ttu-id="bf377-128">tooopen hello voorbeeldcode, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="bf377-128">tooopen hello sample code, follow these steps:</span></span>

1. <span data-ttu-id="bf377-129">Hallo voorbeeld opslagplaats vanuit GitHub door het uitvoeren van de volgende opdracht Hallo klonen:</span><span class="sxs-lookup"><span data-stu-id="bf377-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="bf377-130">Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf377-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="bf377-132">Hallo `app.js` bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toocontrol Hallo LED bevat.</span><span class="sxs-lookup"><span data-stu-id="bf377-132">hello `app.js` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="bf377-133">Afhankelijkheden voor toepassingen installeren</span><span class="sxs-lookup"><span data-stu-id="bf377-133">Install application dependencies</span></span>
<span data-ttu-id="bf377-134">Hallo-bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="bf377-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="bf377-135">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="bf377-135">Configure hello device connection</span></span>
<span data-ttu-id="bf377-136">tooconfigure Hallo apparaatverbinding, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="bf377-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="bf377-137">Hallo apparaat configuratiebestand gegenereerd door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf377-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="bf377-138">Hallo-configuratiebestand `config-raspberrypi.json` Hallo gebruikersreferenties u toolog in tooPi bevat.</span><span class="sxs-lookup"><span data-stu-id="bf377-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="bf377-139">Hallo-geheugenlek tooavoid van gebruikersreferenties, Hallo-configuratiebestand wordt gegenereerd in de submap Hallo `.iot-hub-getting-started` van Hallo basismap op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bf377-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="bf377-140">Hallo apparaat configuratiebestand openen in Visual Studio Code door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf377-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="bf377-141">Vervang Hallo tijdelijke aanduiding voor `[device hostname or IP address]` met Hallo IP-adres of hostnaam Hallo die u eerder hebt verkregen in "Verkrijgen Hallo IP-adres en hostnaam naam van Pi."</span><span class="sxs-lookup"><span data-stu-id="bf377-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="bf377-143">U kunt SSH-sleutel in plaats van de gebruikersnaam en wachtwoord gebruiken wanneer u verbinding maakt tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="bf377-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="bf377-144">In volgorde toodo dit hebt u toogenerate Hallo sleutel met behulp van **ssh-keygen** en **ssh-exemplaar-id pi @\<adres van apparaat\>**.</span><span class="sxs-lookup"><span data-stu-id="bf377-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="bf377-145">In Windows deze opdrachten zijn beschikbaar in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="bf377-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="bf377-146">Op Mac OS moet u toorun **brew installeren ssh-exemplaar-id**.</span><span class="sxs-lookup"><span data-stu-id="bf377-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="bf377-147">Na het uploaden is Hallo sleutel toohello frambozen Pi, Vervang **device_password** met **device_key_path** eigenschap in **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="bf377-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="bf377-148">Bijgewerkte regels ziet er als hieronder:</span><span class="sxs-lookup"><span data-stu-id="bf377-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="bf377-149">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="bf377-149">Congratulations!</span></span> <span data-ttu-id="bf377-150">U hebt gemaakt Hallo eerste voorbeeldtoepassing voor Pi.</span><span class="sxs-lookup"><span data-stu-id="bf377-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="bf377-151">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="bf377-151">Deploy and run hello sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="bf377-152">Node.js en NPM op Pi installeren</span><span class="sxs-lookup"><span data-stu-id="bf377-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="bf377-153">Node.js en NPM met Pi installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf377-153">Install Node.js and NPM on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="bf377-154">Deze taak duurt 10 minuten toocomplete Hallo eerste keer dat u deze uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf377-154">This task might take 10 minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="bf377-155">Implementeren en Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bf377-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="bf377-156">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf377-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="bf377-157">Controleer of de app werkt het Hallo</span><span class="sxs-lookup"><span data-stu-id="bf377-157">Verify hello app works</span></span>
<span data-ttu-id="bf377-158">U ziet nu Hallo LED op Pi knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="bf377-158">You should now see hello LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="bf377-159">Als er geen Hallo LED knippert, raadpleegt u Hallo [probleemoplossingsgids](iot-hub-raspberry-pi-kit-node-troubleshooting.md) voor toocommon oplossingen voor problemen.</span><span class="sxs-lookup"><span data-stu-id="bf377-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="bf377-160">![LED knippert](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="bf377-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="bf377-161">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bf377-161">Summary</span></span>
<span data-ttu-id="bf377-162">U hebt geïnstalleerd Hallo vereist extra toowork met Pi en een voorbeeld toepassing tooPi tooblink Hallo LED geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="bf377-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="bf377-163">U kunt nu maken, implementeren, en voer een ander voorbeeld van een toepassing die verbinding Pi tooAzure toosend IoT Hub maakt en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="bf377-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf377-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf377-164">Next steps</span></span>
[<span data-ttu-id="bf377-165">Hello Azure-hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="bf377-165">Get hello Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

