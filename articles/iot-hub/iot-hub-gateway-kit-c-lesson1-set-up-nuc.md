---
title: 'SensorTag apparaat & Azure IoT Gateway - les 1: Intel NUC instellen | Microsoft Docs'
description: Intel NUC toowork instellen als een IoT-gateway tussen een sensor en Azure IoT Hub toocollect sensor, gegevens en deze tooIoT Hub te verzenden.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT-gateway, intel-nuc nuc computer, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="76f6e-104">Intel NUC instellen als een IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="76f6e-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="76f6e-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="76f6e-105">What you will do</span></span>

- <span data-ttu-id="76f6e-106">Intel NUC instellen als een IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="76f6e-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="76f6e-107">Hello Azure IoT rand pakket installeren op Hallo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="76f6e-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="76f6e-108">Een voorbeeldtoepassing 'hello_world' uitgevoerd op Hallo Intel NUC tooverify Hallo gatewayfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="76f6e-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="76f6e-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="76f6e-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="76f6e-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="76f6e-110">What you will learn</span></span>

<span data-ttu-id="76f6e-111">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="76f6e-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="76f6e-112">Hoe tooconnect Intel NUC met de randapparaten.</span><span class="sxs-lookup"><span data-stu-id="76f6e-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="76f6e-113">Hoe Hallo tooinstall en update vereist hello-pakketten over het gebruik van Intel NUC Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="76f6e-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="76f6e-114">Hoe steekproef toorun Hallo 'hello_world' toepassingsfunctionaliteit tooverify Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="76f6e-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="76f6e-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="76f6e-115">What you need</span></span>

- <span data-ttu-id="76f6e-116">Een Intel NUC Kit DE3815TYKE Hello softwarepakket voor Intel IoT Gateway (o de Linux * 7.0.0.13) vooraf is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="76f6e-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="76f6e-117">[Klik hier toopurchase Groove IoT commerciële Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="76f6e-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="76f6e-118">Een Ethernet-kabel.</span><span class="sxs-lookup"><span data-stu-id="76f6e-118">An Ethernet cable.</span></span>
- <span data-ttu-id="76f6e-119">Een toetsenbord.</span><span class="sxs-lookup"><span data-stu-id="76f6e-119">A keyboard.</span></span>
- <span data-ttu-id="76f6e-120">Een HDMI of VGA-kabel.</span><span class="sxs-lookup"><span data-stu-id="76f6e-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="76f6e-121">Een monitor met een HDMI of VGA-poort.</span><span class="sxs-lookup"><span data-stu-id="76f6e-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="76f6e-122">Optioneel: [Texas instrumenten Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="76f6e-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Gateway-pakket](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="76f6e-124">Intel NUC verbinding met de randapparaten Hallo</span><span class="sxs-lookup"><span data-stu-id="76f6e-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="76f6e-125">Hallo in onderstaande afbeelding is een voorbeeld van Intel NUC die is verbonden met verschillende randapparatuur:</span><span class="sxs-lookup"><span data-stu-id="76f6e-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="76f6e-126">Verbonden tooa toetsenbord.</span><span class="sxs-lookup"><span data-stu-id="76f6e-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="76f6e-127">Monitor tooa verbonden met een VGA-kabel of HDMI-kabel.</span><span class="sxs-lookup"><span data-stu-id="76f6e-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="76f6e-128">Verbonden tooa bekabelde netwerk met een Ethernet-kabel.</span><span class="sxs-lookup"><span data-stu-id="76f6e-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="76f6e-129">Voeding tooa verbonden met een power-kabel.</span><span class="sxs-lookup"><span data-stu-id="76f6e-129">Connected tooa power supply with a power cable.</span></span>

![Intel NUC tooperipherals verbonden](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="76f6e-131">Verbinding maken met toohello Intel NUC systeem van de hostcomputer via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="76f6e-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="76f6e-132">U moet een toetsenbord en een monitor tooget Hallo IP-adres van uw apparaat Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="76f6e-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="76f6e-133">Als u Hallo IP weet-adres, kunt u vooruit toostep 3 in deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="76f6e-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="76f6e-134">Hallo Intel NUC inschakelen door te drukken Hallo / uit-knop en meld u vervolgens aan.</span><span class="sxs-lookup"><span data-stu-id="76f6e-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="76f6e-135">Hallo standaard-gebruikersnaam en wachtwoord zijn beide `root`.</span><span class="sxs-lookup"><span data-stu-id="76f6e-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="76f6e-136">Hallo IP-adres van Hallo Intel NUC ophalen door het uitvoeren van Hallo `ifconfig` opdracht op Hallo Intel NUC apparaat.</span><span class="sxs-lookup"><span data-stu-id="76f6e-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="76f6e-137">Hier volgt een voorbeeld van uitvoer van de opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="76f6e-137">Here is an example of hello command output.</span></span>

   ![ifconfig-uitvoer met Intel NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="76f6e-139">In dit voorbeeld Hallo waarde die volgt `inet addr:` Hallo IP-adres is die u nodig hebt wanneer een verbinding tussen toohello Intel NUC van een hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="76f6e-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="76f6e-140">Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooIntel NUC Hallo.</span><span class="sxs-lookup"><span data-stu-id="76f6e-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="76f6e-141">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="76f6e-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="76f6e-142">Hallo ingebouwde SSH-client op Ubuntu- of Mac OS.</span><span class="sxs-lookup"><span data-stu-id="76f6e-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="76f6e-143">Het is efficiënter en productiever toooperate een Intel NUC van een hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="76f6e-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="76f6e-144">U zult nodig Hallo Intel NUC van IP-adres, gebruiker en het wachtwoord tooconnect tooit via een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="76f6e-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="76f6e-145">Hier volgt een voorbeeld dat gebruikmaakt van een SSH-client op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="76f6e-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="76f6e-146">![SSH-client op Mac OS uitgevoerd](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="76f6e-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="76f6e-147">Hello Azure IoT rand pakket installeren</span><span class="sxs-lookup"><span data-stu-id="76f6e-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="76f6e-148">Hello Azure IoT rand pakket bevat de binaire bestanden voor Hallo vooraf gecompileerde van IoT-rand en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="76f6e-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="76f6e-149">Deze binaire bestanden zijn Azure IoT Edge, hello Azure IoT SDK en Hallo bijbehorende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="76f6e-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="76f6e-150">Hallo pakket bevat ook een 'hello_world' is gebruikte toovalidate Hallo gatewayfunctionaliteit voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="76f6e-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="76f6e-151">IoT-rand Hallo core deel uitmaakt van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="76f6e-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="76f6e-152">Volg deze stappen tooinstall Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="76f6e-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="76f6e-153">Hallo IoT Cloud-opslagplaats toevoegen door het uitvoeren van de volgende opdrachten in een terminalvenster Hallo:</span><span class="sxs-lookup"><span data-stu-id="76f6e-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="76f6e-154">Voer 'y' als too'Include vraagt dit kanaal?'</span><span class="sxs-lookup"><span data-stu-id="76f6e-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="76f6e-155">Als u krijgt een `import read failed(-1)` gebruik Hallo opdrachten tooresolve Hallo probleem volgende fout is opgetreden:</span><span class="sxs-lookup"><span data-stu-id="76f6e-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="76f6e-156">Hallo `rpm` opdracht invoer Hallo rpm-sleutel.</span><span class="sxs-lookup"><span data-stu-id="76f6e-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="76f6e-157">Hallo `smart channel` opdracht voegt Hallo rpm channel toohello Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="76f6e-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="76f6e-158">Voordat u Hallo uitvoert `smart update` uitvoert, ziet u uitvoer zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="76f6e-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![rpm en slimme kanaal opdrachten uitvoer](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="76f6e-160">Hallo smart update-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="76f6e-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="76f6e-161">Hello Azure IoT Gateway-pakket installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="76f6e-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="76f6e-162">`packagegroup-cloud-azure`Hallo-naam van het Hallo-pakket is.</span><span class="sxs-lookup"><span data-stu-id="76f6e-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="76f6e-163">Hallo `smart install` opdracht gebruikte tooinstall Hallo pakket is.</span><span class="sxs-lookup"><span data-stu-id="76f6e-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="76f6e-164">Voer Hallo volgende opdracht uit als u deze fout te zien: 'openbare sleutel niet beschikbaar'</span><span class="sxs-lookup"><span data-stu-id="76f6e-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="76f6e-165">Hallo Intel NUC opnieuw opstarten als u deze fout ziet: 'Er is geen pakket biedt util-linux-dev'</span><span class="sxs-lookup"><span data-stu-id="76f6e-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="76f6e-166">Nadat het Hallo-pakket is geïnstalleerd, is Intel NUC gereed toofunction als een gateway.</span><span class="sxs-lookup"><span data-stu-id="76f6e-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="76f6e-167">Hello Azure IoT Edge 'hello_world' voorbeeld van een toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="76f6e-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="76f6e-168">Hallo volgende voorbeeld van een toepassing maakt een gateway vanuit een `hello_world.json` bestands- en Hallo fundamentele onderdelen van Azure IoT rand architectuur toolog een hello world tooa berichtbestand (log.txt) gebruikt om de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="76f6e-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="76f6e-169">U kunt Hallo Hallo wereld-voorbeeld uitvoeren door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="76f6e-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="76f6e-170">Hallo wereld Hallo-toepassing uitvoeren voor een paar minuten en klik vervolgens op Hallo Enter key toostop, kunnen deze.</span><span class="sxs-lookup"><span data-stu-id="76f6e-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="76f6e-171">![uitvoer van de toepassing](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="76f6e-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="76f6e-172">U kunt negeren 'ongeldig argument handle(NULL)' fouten die worden weergegeven nadat u druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="76f6e-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="76f6e-173">U kunt controleren dat Hallo-gateway is uitgevoerd door het openen van Hallo log.txt-bestand dat is nu in de map hello_world ![log.txt directory weergeven](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="76f6e-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="76f6e-174">Open log.txt Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="76f6e-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="76f6e-175">Vervolgens ziet u Hallo inhoud van log.txt die als een JSON-indeling uitvoer van Hallo berichtregistratie die elke vijf seconden module voor gateway Hallo wereld Hallo zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="76f6e-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="76f6e-176">![log.txt directory weergeven](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="76f6e-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="76f6e-177">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="76f6e-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="76f6e-178">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="76f6e-178">Summary</span></span>

<span data-ttu-id="76f6e-179">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="76f6e-179">Congratulations!</span></span> <span data-ttu-id="76f6e-180">U klaar bent met het instellen van Intel NUC als een gateway.</span><span class="sxs-lookup"><span data-stu-id="76f6e-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="76f6e-181">Nu u klaar toomove op de volgende les tooset toohello uw hostcomputer van de bent, een Azure-IoT-Hub maken en registreren van uw logische Azure IoT Hub-apparaat.</span><span class="sxs-lookup"><span data-stu-id="76f6e-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76f6e-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76f6e-182">Next steps</span></span>
[<span data-ttu-id="76f6e-183">Een IoT gateway tooconnect een apparaat tooAzure IoT Hub gebruiken</span><span class="sxs-lookup"><span data-stu-id="76f6e-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

