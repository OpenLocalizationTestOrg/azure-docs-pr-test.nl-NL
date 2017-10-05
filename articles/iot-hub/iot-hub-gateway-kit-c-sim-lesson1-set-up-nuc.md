---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 1: NUC instellen | Microsoft Docs'
description: Intel NUC instellen om te werken als een IoT-gateway tussen een sensor en Azure IoT Hub sensor gegevens kunt verzamelen en verzenden naar IoT Hub.
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="e9b71-104">Intel NUC instellen als een IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="e9b71-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e9b71-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="e9b71-105">What you will do</span></span>

- <span data-ttu-id="e9b71-106">Intel NUC instellen als een IoT-gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="e9b71-107">Installeer het pakket Azure IoT Edge op Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="e9b71-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="e9b71-108">Voer een voorbeeldtoepassing 'hello_world' op Intel NUC om te controleren of de functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="e9b71-109">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e9b71-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e9b71-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="e9b71-110">What you will learn</span></span>

<span data-ttu-id="e9b71-111">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="e9b71-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="e9b71-112">Klik hier voor meer informatie over het Intel NUC verbinding met de randapparaten.</span><span class="sxs-lookup"><span data-stu-id="e9b71-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="e9b71-113">Informatie over het installeren en bijwerken van de vereiste pakketten op Intel NUC met behulp van de smartcard Package Manager.</span><span class="sxs-lookup"><span data-stu-id="e9b71-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="e9b71-114">Het uitvoeren van de voorbeeldtoepassing 'hello_world' om te controleren of de functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9b71-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="e9b71-115">What you need</span></span>

- <span data-ttu-id="e9b71-116">Een Intel NUC Kit DE3815TYKE met Intel IoT Gateway Software Suite (o de Linux * 7.0.0.13) vooraf is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e9b71-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="e9b71-117">Een Ethernet-kabel.</span><span class="sxs-lookup"><span data-stu-id="e9b71-117">An Ethernet cable.</span></span>
- <span data-ttu-id="e9b71-118">Een toetsenbord.</span><span class="sxs-lookup"><span data-stu-id="e9b71-118">A keyboard.</span></span>
- <span data-ttu-id="e9b71-119">Een HDMI of VGA-kabel.</span><span class="sxs-lookup"><span data-stu-id="e9b71-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="e9b71-120">Een monitor met een HDMI of VGA-poort.</span><span class="sxs-lookup"><span data-stu-id="e9b71-120">A monitor with an HDMI or VGA port.</span></span>

![Gateway-pakket](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="e9b71-122">Intel NUC verbinden met de randapparaten</span><span class="sxs-lookup"><span data-stu-id="e9b71-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="e9b71-123">De onderstaande afbeelding is een voorbeeld van Intel NUC die is verbonden met verschillende randapparatuur:</span><span class="sxs-lookup"><span data-stu-id="e9b71-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="e9b71-124">Verbonden met een toetsenbord.</span><span class="sxs-lookup"><span data-stu-id="e9b71-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="e9b71-125">Verbonden met de monitor door een VGA-kabel of HDMI-kabel.</span><span class="sxs-lookup"><span data-stu-id="e9b71-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="e9b71-126">Verbonden met een bekabeld netwerk door een Ethernet-kabel.</span><span class="sxs-lookup"><span data-stu-id="e9b71-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="e9b71-127">Verbonden met de voeding met een power-kabel.</span><span class="sxs-lookup"><span data-stu-id="e9b71-127">Connected to the power supply with a power cable.</span></span>

![Intel NUC verbonden met de randapparaten](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="e9b71-129">Verbinding maken met de Intel NUC-systeem van de hostcomputer via Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="e9b71-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="e9b71-130">U moet hier toetsenbord en de monitor voor het IP-adres van uw apparaat NUC ophalen.</span><span class="sxs-lookup"><span data-stu-id="e9b71-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="e9b71-131">Als u het IP-adres al weet, kunt u naar stap 3 in deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="e9b71-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="e9b71-132">Intel NUC inschakelen door op de knop Power en meld u bij het systeem.</span><span class="sxs-lookup"><span data-stu-id="e9b71-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="e9b71-133">De standaard-gebruikersnaam en wachtwoord zijn beide `root`.</span><span class="sxs-lookup"><span data-stu-id="e9b71-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="e9b71-134">Het IP-adres van NUC ophalen door het uitvoeren van de `ifconfig` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e9b71-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="e9b71-135">Deze stap wordt uitgevoerd op het apparaat NUC.</span><span class="sxs-lookup"><span data-stu-id="e9b71-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="e9b71-136">Hier volgt een voorbeeld van uitvoer van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="e9b71-136">Here is an example of the command output.</span></span>

   ![ifconfig-uitvoer met NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="e9b71-138">In dit voorbeeld wordt de waarde die volgt `inet addr:` is het IP-adres dat u nodig hebt wanneer u van plan bent extern verbinding kunnen maken van een hostcomputer te Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="e9b71-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="e9b71-139">Gebruik een van de volgende SSH-clients van uw hostmachine verbinding maken met de Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="e9b71-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="e9b71-140">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="e9b71-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="e9b71-141">De build in SSH-client op Ubuntu- of Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e9b71-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="e9b71-142">Het is efficiënter en productiever bewerkingen uitvoeren op Intel NUC van een hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="e9b71-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="e9b71-143">U moet het de IP-adres, gebruikersnaam en wachtwoord voor het verbinding maken met de NUC via SSH-client.</span><span class="sxs-lookup"><span data-stu-id="e9b71-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="e9b71-144">Hier volgt de voorbeeld gebruik SSH-client op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e9b71-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="e9b71-145">![SSH-client op Mac OS uitgevoerd](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="e9b71-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="e9b71-146">Installeer het Azure IoT Edge-pakket</span><span class="sxs-lookup"><span data-stu-id="e9b71-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="e9b71-147">Het Azure-IoT-Edge-pakket bevat de vooraf gecompileerde binaire bestanden van de SDK en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e9b71-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="e9b71-148">Deze binaire bestanden zijn Azure IoT Edge, de Azure IoT SDK en de bijbehorende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="e9b71-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="e9b71-149">Het pakket bevat ook een 'hello_world'-voorbeeldtoepassing die wordt gebruikt voor het valideren van de functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="e9b71-150">IoT-rand is het belangrijkste deel van de gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="e9b71-151">Volg deze stappen voor het installeren van het pakket:</span><span class="sxs-lookup"><span data-stu-id="e9b71-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="e9b71-152">De IoT-cloud-opslagplaats met de volgende opdrachten in een terminalvenster toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e9b71-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="e9b71-153">De `rpm` opdracht wordt de sleutel rpm geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="e9b71-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="e9b71-154">De `smart channel` opdracht voegt het rpm-kanaal naar de smartcard Package Manager.</span><span class="sxs-lookup"><span data-stu-id="e9b71-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="e9b71-155">Voordat u de `smart update` opdracht, ziet u uitvoer zoals hieronder.</span><span class="sxs-lookup"><span data-stu-id="e9b71-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![rpm en slimme kanaal opdrachten uitvoer](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="e9b71-157">Installeer het pakket met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e9b71-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="e9b71-158">`packagegroup-cloud-azure`is de naam van het pakket.</span><span class="sxs-lookup"><span data-stu-id="e9b71-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="e9b71-159">De `smart install` opdracht wordt gebruikt om het pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="e9b71-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="e9b71-160">Nadat het pakket is geïnstalleerd, Intel NUC naar verwachting werken als een gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="e9b71-161">De voorbeeldtoepassing voor Azure IoT Edge 'hello_world' uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e9b71-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="e9b71-162">Ga naar `azureiotgatewaysdk/samples` en de voorbeeldtoepassing 'hello_world' in het voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="e9b71-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="e9b71-163">Deze voorbeeldtoepassing maakt u een gateway vanuit de `hello_world.json` bestand en de fundamentele onderdelen van de rand van Azure IoT-architectuur gebruikt voor het vastleggen van een Hallo wereld-bericht in een bestand om de vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="e9b71-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="e9b71-164">U kunt de voorbeeldtoepassing 'hello_world'-voorbeeld uitvoeren door met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e9b71-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="e9b71-165">Als de functionaliteit van de gateway correct werkt, wordt de voorbeeldtoepassing in de volgende uitvoer gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="e9b71-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![uitvoer van de toepassing](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="e9b71-167">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e9b71-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="e9b71-168">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="e9b71-168">Summary</span></span>

<span data-ttu-id="e9b71-169">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="e9b71-169">Congratulations!</span></span> <span data-ttu-id="e9b71-170">U klaar bent met het instellen van Intel NUC als een gateway.</span><span class="sxs-lookup"><span data-stu-id="e9b71-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="e9b71-171">U kunt nu klaar om door te gaan met de volgende les instellen van de hostcomputer, een Azure IoT hub maken en registreren van uw logische Azure IoT hub-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e9b71-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9b71-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9b71-172">Next steps</span></span>
[<span data-ttu-id="e9b71-173">Bereid u voor uw hostcomputer en Azure IoT hub</span><span class="sxs-lookup"><span data-stu-id="e9b71-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
