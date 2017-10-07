---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 1: NUC instellen | Microsoft Docs'
description: Intel NUC toowork instellen als een IoT-gateway tussen een sensor en Azure IoT Hub toocollect sensor, gegevens en deze tooIoT Hub te verzenden.
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: IOT-gateway, intel-nuc nuc computer, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="46007-104">Intel NUC instellen als een IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="46007-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="46007-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="46007-105">What you will do</span></span>

- <span data-ttu-id="46007-106">Intel NUC instellen als een IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="46007-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="46007-107">Hello Azure IoT rand pakket installeren op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="46007-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="46007-108">Een voorbeeldtoepassing 'hello_world' uitgevoerd op Intel NUC tooverify Hallo gatewayfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="46007-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="46007-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="46007-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="46007-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="46007-110">What you will learn</span></span>

<span data-ttu-id="46007-111">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="46007-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="46007-112">Hoe tooconnect Intel NUC met de randapparaten.</span><span class="sxs-lookup"><span data-stu-id="46007-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="46007-113">Hoe Hallo tooinstall en update vereist hello-pakketten over het gebruik van Intel NUC Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="46007-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="46007-114">Hoe steekproef toorun Hallo 'hello_world' toepassingsfunctionaliteit tooverify Hallo gateway.</span><span class="sxs-lookup"><span data-stu-id="46007-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="46007-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="46007-115">What you need</span></span>

- <span data-ttu-id="46007-116">Een Intel NUC Kit DE3815TYKE Hello softwarepakket voor Intel IoT Gateway (o de Linux * 7.0.0.13) vooraf is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="46007-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="46007-117">Een Ethernet-kabel.</span><span class="sxs-lookup"><span data-stu-id="46007-117">An Ethernet cable.</span></span>
- <span data-ttu-id="46007-118">Een toetsenbord.</span><span class="sxs-lookup"><span data-stu-id="46007-118">A keyboard.</span></span>
- <span data-ttu-id="46007-119">Een HDMI of VGA-kabel.</span><span class="sxs-lookup"><span data-stu-id="46007-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="46007-120">Een monitor met een HDMI of VGA-poort.</span><span class="sxs-lookup"><span data-stu-id="46007-120">A monitor with an HDMI or VGA port.</span></span>

![Gateway-pakket](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="46007-122">Intel NUC verbinding met de randapparaten Hallo</span><span class="sxs-lookup"><span data-stu-id="46007-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="46007-123">Hallo in onderstaande afbeelding is een voorbeeld van Intel NUC die is verbonden met verschillende randapparatuur:</span><span class="sxs-lookup"><span data-stu-id="46007-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="46007-124">Verbonden tooa toetsenbord.</span><span class="sxs-lookup"><span data-stu-id="46007-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="46007-125">Verbonden toohello monitor door een VGA-kabel of HDMI-kabel.</span><span class="sxs-lookup"><span data-stu-id="46007-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="46007-126">Verbonden tooa bekabelde netwerk door een Ethernet-kabel.</span><span class="sxs-lookup"><span data-stu-id="46007-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="46007-127">Voeding toohello verbonden met een power-kabel.</span><span class="sxs-lookup"><span data-stu-id="46007-127">Connected toohello power supply with a power cable.</span></span>

![Intel NUC tooperipherals verbonden](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="46007-129">Verbinding maken met toohello Intel NUC systeem van de hostcomputer via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="46007-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="46007-130">Hier moet u een toetsenbord en monitor tooget Hallo IP-adres van uw apparaat NUC.</span><span class="sxs-lookup"><span data-stu-id="46007-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="46007-131">Als u Hallo IP weet-adres, kunt u toostep 3 in deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="46007-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="46007-132">Intel NUC inschakelen door op Hallo / uit-knop en logboekbestanden op Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="46007-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="46007-133">Hallo standaard-gebruikersnaam en wachtwoord zijn beide `root`.</span><span class="sxs-lookup"><span data-stu-id="46007-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="46007-134">Hallo IP-adres van NUC ophalen door het uitvoeren van Hallo `ifconfig` opdracht.</span><span class="sxs-lookup"><span data-stu-id="46007-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="46007-135">Deze stap wordt uitgevoerd op Hallo NUC apparaat.</span><span class="sxs-lookup"><span data-stu-id="46007-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="46007-136">Hier volgt een voorbeeld van uitvoer van de opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="46007-136">Here is an example of hello command output.</span></span>

   ![ifconfig-uitvoer met NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="46007-138">In dit voorbeeld Hallo waarde die volgt `inet addr:` Hallo IP-adres dat u nodig hebt wanneer u van plan tooconnect extern vanaf een host computer tooIntel NUC bent.</span><span class="sxs-lookup"><span data-stu-id="46007-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="46007-139">Gebruik een van de volgende clients SSH uit uw host machine tooconnect tooIntel NUC Hallo.</span><span class="sxs-lookup"><span data-stu-id="46007-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="46007-140">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="46007-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="46007-141">Hallo build in SSH-client op Ubuntu- of Mac OS.</span><span class="sxs-lookup"><span data-stu-id="46007-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="46007-142">Het is efficiënter en productiever toooperate op Intel NUC van een hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="46007-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="46007-143">U moet Hallo Hallo IP-adres, gebruikersnaam en wachtwoord tooconnect hello NUC via SSH-client.</span><span class="sxs-lookup"><span data-stu-id="46007-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="46007-144">Hier volgt Hallo voorbeeld gebruik SSH-client op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="46007-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="46007-145">![SSH-client op Mac OS uitgevoerd](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="46007-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="46007-146">Hello Azure IoT rand pakket installeren</span><span class="sxs-lookup"><span data-stu-id="46007-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="46007-147">Hello Azure IoT rand pakket bevat de binaire bestanden voor Hallo vooraf gecompileerde Hallo SDK en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="46007-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="46007-148">Deze binaire bestanden zijn Azure IoT Edge, hello Azure IoT SDK en Hallo bijbehorende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="46007-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="46007-149">Hallo-pakket bevat ook een 'hello_world'-voorbeeldtoepassing die is gebruikt toovalidate Hallo gatewayfunctionaliteit.</span><span class="sxs-lookup"><span data-stu-id="46007-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="46007-150">IoT-rand Hallo core deel uitmaakt van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="46007-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="46007-151">tooinstall Hallo van het pakket, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="46007-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="46007-152">Hallo IoT cloud opslagplaats toevoegen door het uitvoeren van de volgende opdrachten in een terminalvenster Hallo:</span><span class="sxs-lookup"><span data-stu-id="46007-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="46007-153">Hallo `rpm` opdracht invoer Hallo rpm-sleutel.</span><span class="sxs-lookup"><span data-stu-id="46007-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="46007-154">Hallo `smart channel` opdracht voegt Hallo rpm channel toohello Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="46007-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="46007-155">Voordat u Hallo uitvoert `smart update` opdracht, ziet u uitvoer zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="46007-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![rpm en slimme kanaal opdrachten uitvoer](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="46007-157">Hallo-pakket installeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="46007-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="46007-158">`packagegroup-cloud-azure`Hallo-naam van het Hallo-pakket is.</span><span class="sxs-lookup"><span data-stu-id="46007-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="46007-159">Hallo `smart install` opdracht gebruikte tooinstall Hallo pakket is.</span><span class="sxs-lookup"><span data-stu-id="46007-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="46007-160">Nadat het Hallo-pakket is geïnstalleerd, is Intel NUC verwachte toowork als een gateway.</span><span class="sxs-lookup"><span data-stu-id="46007-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="46007-161">Hello Azure IoT Edge 'hello_world' voorbeeld van een toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="46007-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="46007-162">Ga te`azureiotgatewaysdk/samples` en voer 'hello_world' Hallo-voorbeeld voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="46007-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="46007-163">Deze voorbeeldtoepassing een gateway maakt van Hallo `hello_world.json` bestands- en Hallo fundamentele onderdelen van hello Azure IoT rand architectuur toolog een Hallo wereld berichtbestand tooa gebruikt om de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="46007-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="46007-164">U kunt 'hello_world' Hallo-voorbeeld voorbeeldtoepassing uitvoeren door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="46007-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="46007-165">Hallo-voorbeeldtoepassing produceert Hallo volgende uitvoer als Hallo gatewayfunctionaliteit correct werkt:</span><span class="sxs-lookup"><span data-stu-id="46007-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![uitvoer van de toepassing](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="46007-167">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="46007-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="46007-168">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="46007-168">Summary</span></span>

<span data-ttu-id="46007-169">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="46007-169">Congratulations!</span></span> <span data-ttu-id="46007-170">U klaar bent met het instellen van Intel NUC als een gateway.</span><span class="sxs-lookup"><span data-stu-id="46007-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="46007-171">Nu kunt u nu wordt toomove op het volgende les tooset toohello van uw hostcomputer maken van een Azure-IoT-hub en Registreer uw logische Azure IoT hub-apparaat.</span><span class="sxs-lookup"><span data-stu-id="46007-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46007-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46007-172">Next steps</span></span>
[<span data-ttu-id="46007-173">Bereid u voor uw hostcomputer en Azure IoT hub</span><span class="sxs-lookup"><span data-stu-id="46007-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
