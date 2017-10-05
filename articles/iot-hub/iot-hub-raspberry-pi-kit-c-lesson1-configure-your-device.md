---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Frambozen Pi 3 configureren voor gebruik van de eerste en het besturingssysteem Raspbian, een gratis besturingssysteem dat is geoptimaliseerd voor de hardware frambozen Pi installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: installatie raspbian, raspbian downloaden waarop voor het installeren van raspbian, raspbian setup, raspberry pi installeren raspbian, raspberry pi installeren os, raspberry pi sd-kaart installeren, frambozen pi verbinding maken, verbinding maken met raspberry pi raspberry pi connectiviteit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="b1a2d-104">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="b1a2d-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b1a2d-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="b1a2d-105">What you will do</span></span>
<span data-ttu-id="b1a2d-106">Pi configureren voor het eerste gebruik en het besturingssysteem Raspbian installeren.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="b1a2d-107">Raspbian is een gratis besturingssysteem die is geoptimaliseerd voor de hardware frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="b1a2d-108">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b1a2d-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b1a2d-109">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="b1a2d-109">What you will learn</span></span>
<span data-ttu-id="b1a2d-110">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="b1a2d-110">In this article, you will learn:</span></span>

* <span data-ttu-id="b1a2d-111">Het installeren van Raspbian op Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="b1a2d-112">Klik hier voor meer informatie over het opstarten van Pi via een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="b1a2d-113">Klik hier voor meer informatie over het Pi verbinding met het netwerk met behulp van een Ethernet-kabel of draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="b1a2d-114">Hoe een LED toevoegen aan de breadboard en te verbinden met Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b1a2d-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="b1a2d-115">What you need</span></span>
<span data-ttu-id="b1a2d-116">Om deze bewerking niet voltooien, moet u de volgende onderdelen van uw frambozen Pi 3 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="b1a2d-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="b1a2d-117">De kaart frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="b1a2d-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="b1a2d-118">De 16 GB microSD-kaart</span><span class="sxs-lookup"><span data-stu-id="b1a2d-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="b1a2d-119">De 5-v 2 amp power supply met 6 mond micro USB-kabel</span><span class="sxs-lookup"><span data-stu-id="b1a2d-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="b1a2d-120">De breadboard</span><span class="sxs-lookup"><span data-stu-id="b1a2d-120">The breadboard</span></span>
* <span data-ttu-id="b1a2d-121">Connector-kabels</span><span class="sxs-lookup"><span data-stu-id="b1a2d-121">Connector wires</span></span>
* <span data-ttu-id="b1a2d-122">Een weerstand 560 ohm</span><span class="sxs-lookup"><span data-stu-id="b1a2d-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="b1a2d-123">Een gedempt 10 mm LED</span><span class="sxs-lookup"><span data-stu-id="b1a2d-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="b1a2d-124">De Ethernet-kabel</span><span class="sxs-lookup"><span data-stu-id="b1a2d-124">The Ethernet cable</span></span>

![Dingen in uw starterskit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="b1a2d-126">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="b1a2d-126">You also need:</span></span>

* <span data-ttu-id="b1a2d-127">Een bekabelde of draadloze verbinding voor Pi verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="b1a2d-128">Een USB-SD adapter of mini-SD-kaart zet de OS-installatiekopie op de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="b1a2d-129">Een computer met Windows, Mac of Linux.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="b1a2d-130">De computer wordt gebruikt voor het installeren van Raspbian op de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="b1a2d-131">Een internetverbinding beschikken om het downloaden van de benodigde hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="b1a2d-132">Raspbian installeren op de MicroSD-kaart</span><span class="sxs-lookup"><span data-stu-id="b1a2d-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="b1a2d-133">Bereid de microSD-kaart voor de installatie van de installatiekopie van het Raspbian.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="b1a2d-134">Raspbian downloaden.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="b1a2d-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) het ZIP-bestand voor Raspbian Jessie met Pixel.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="b1a2d-136">Pak de installatiekopie van het Raspbian naar een map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="b1a2d-137">Installeer Raspbian naar de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="b1a2d-138">[Download](https://www.etcher.io) en installeer het hulpprogramma Etcher SD-kaart brander.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="b1a2d-139">Voer Etcher en selecteer de installatiekopie van het Raspbian die u hebt opgehaald in stap 1.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="b1a2d-140">Selecteer het station microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="b1a2d-141">Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd de juiste station.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="b1a2d-142">Klik op **Flash** Raspbian installeren op de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="b1a2d-143">Verwijder de microSD-kaart van uw computer wanneer de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="b1a2d-144">Het is veilig worden verwijderd, de microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of ontkoppelt de microSD-kaart is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="b1a2d-145">De microSD-kaart invoegen in uw Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-145">Insert the microSD card into your Pi.</span></span>

![Invoegen van de SD-kaart](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="b1a2d-147">Pi inschakelen</span><span class="sxs-lookup"><span data-stu-id="b1a2d-147">Turn on Pi</span></span>
<span data-ttu-id="b1a2d-148">Pi inschakelen met behulp van het micro USB-kabel en de voeding.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Inschakelen](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="b1a2d-150">Het is belangrijk dat u de voeding in de kit ten minste 2A om ervoor te zorgen dat uw frambozen heeft onvoldoende stroom correct te laten werken.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="b1a2d-151">SSH inschakelen</span><span class="sxs-lookup"><span data-stu-id="b1a2d-151">Enable SSH</span></span>
<span data-ttu-id="b1a2d-152">Vanaf de release van November 2016 heeft Raspbian de SSH-server standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="b1a2d-153">U moet handmatig inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-153">You need to enable it manually.</span></span> <span data-ttu-id="b1a2d-154">U kunt verwijzen naar de [officiële instructies](https://www.raspberrypi.org/documentation/remote-access/ssh/) of verbinding maken met een monitor en Ga naar **Voorkeuren -> frambozen Pi configuratie** SSH inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="b1a2d-155">Frambozen Pi 3 verbinding met het netwerk</span><span class="sxs-lookup"><span data-stu-id="b1a2d-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="b1a2d-156">U kunt Pi verbinding maken met een bekabeld netwerk of een draadloos netwerk.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="b1a2d-157">Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="b1a2d-158">U kunt bijvoorbeeld Pi verbinden met dezelfde switch waarmee uw computer is verbonden.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="b1a2d-159">Verbinding maken met een bekabeld netwerk</span><span class="sxs-lookup"><span data-stu-id="b1a2d-159">Connect to a wired network</span></span>
<span data-ttu-id="b1a2d-160">Via het Ethernet-kabel Pi verbinden met het bekabelde netwerk.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="b1a2d-161">De twee LED's met Pi inschakelen als de verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Verbinding maken met behulp van een Ethernet-kabel](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="b1a2d-163">Verbinding maken met een draadloos netwerk</span><span class="sxs-lookup"><span data-stu-id="b1a2d-163">Connect to a wireless network</span></span>
<span data-ttu-id="b1a2d-164">Ga als volgt de [instructies](https://www.raspberrypi.org/learning/software-guide/wifi/) van de Stichting frambozen Pi Pi verbinding met uw draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="b1a2d-165">Deze instructies, moet u eerst een verbinding tussen een monitor en een toetsenbord tot Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="b1a2d-166">Verbinding maken met de LED Pi</span><span class="sxs-lookup"><span data-stu-id="b1a2d-166">Connect the LED to Pi</span></span>
<span data-ttu-id="b1a2d-167">Gebruik voor het voltooien van deze taak de [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), de kabels connector, de LED en de weerstand.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="b1a2d-168">Verbind ze naar de [voor algemene doeleinden input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO)-poorten van Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard LED en weerstand](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="b1a2d-170">Verbinding maken met de kortere zijde van de LED naar **GPIO GND (pincode 6)**.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="b1a2d-171">Verbinding maken met de langer zijde van de LED één arm van de weerstand.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="b1a2d-172">Verbinding maken met de andere zijde van de weerstand naar **GPIO 4 (7 pincode)**.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="b1a2d-173">Houd er rekening mee dat de polariteit LED belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="b1a2d-174">Deze instelling polariteit staat bekend als actief laag.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-174">This polarity setting is commonly known as Active Low.</span></span>

![Pin-out](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="b1a2d-176">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-176">Congratulations!</span></span> <span data-ttu-id="b1a2d-177">U hebt geconfigureerd Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="b1a2d-178">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b1a2d-178">Summary</span></span>
<span data-ttu-id="b1a2d-179">In dit artikel hebt u geleerd hoe Pi configureren met Raspbian installeren en verbinding maken met een LED Pi Pi verbinden met een netwerk.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="b1a2d-180">Houd er rekening mee dat de LED nog niet branden.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="b1a2d-181">De volgende taak is het installeren van de benodigde hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="b1a2d-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Hardware is gereed](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="b1a2d-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1a2d-183">Next steps</span></span>
[<span data-ttu-id="b1a2d-184">Download de hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="b1a2d-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

