---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Frambozen Pi 3 configureren voor gebruik van de eerste keer en Hallo Raspbian OS een gratis besturingssysteem dat is geoptimaliseerd voor Hallo frambozen Pi hardware installeren.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: installatie raspbian, raspbian downloaden waarop tooinstall raspbian, raspbian setup raspberry pi installeren raspbian raspberry pi installeren os raspberry pi sd-kaart installeren, raspberry pi verbinding maken, verbinding tooraspberry pi raspberry pi connectiviteit
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
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="d15ed-104">Uw apparaat configureren</span><span class="sxs-lookup"><span data-stu-id="d15ed-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d15ed-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="d15ed-105">What you will do</span></span>
<span data-ttu-id="d15ed-106">Pi configureren voor gebruik van de eerste keer en Hallo Raspbian besturingssysteem installeren.</span><span class="sxs-lookup"><span data-stu-id="d15ed-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="d15ed-107">Raspbian is een gratis besturingssysteem die is geoptimaliseerd voor Hallo frambozen Pi hardware.</span><span class="sxs-lookup"><span data-stu-id="d15ed-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="d15ed-108">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d15ed-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d15ed-109">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="d15ed-109">What you will learn</span></span>
<span data-ttu-id="d15ed-110">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="d15ed-110">In this article, you will learn:</span></span>

* <span data-ttu-id="d15ed-111">Hoe tooinstall Raspbian met Pi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="d15ed-112">Hoe toopower up Pi via een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="d15ed-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="d15ed-113">Hoe tooconnect Pi toohello netwerk met behulp van een Ethernet-kabel of draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="d15ed-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="d15ed-114">Hoe een LED toohello tooadd breadboard en verbind deze tooPi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d15ed-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="d15ed-115">What you need</span></span>
<span data-ttu-id="d15ed-116">toocomplete deze bewerking moet u volgende onderdelen van uw frambozen Pi 3 Starter Kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="d15ed-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="d15ed-117">Hallo frambozen Pi 3 mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="d15ed-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="d15ed-118">Hallo 16 GB microSD-kaart</span><span class="sxs-lookup"><span data-stu-id="d15ed-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="d15ed-119">Hallo 5 v 2 amp voeding met Hallo 6 mond micro USB-kabel</span><span class="sxs-lookup"><span data-stu-id="d15ed-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="d15ed-120">Hallo breadboard</span><span class="sxs-lookup"><span data-stu-id="d15ed-120">hello breadboard</span></span>
* <span data-ttu-id="d15ed-121">Connector-kabels</span><span class="sxs-lookup"><span data-stu-id="d15ed-121">Connector wires</span></span>
* <span data-ttu-id="d15ed-122">Een weerstand 560 ohm</span><span class="sxs-lookup"><span data-stu-id="d15ed-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="d15ed-123">Een gedempt 10 mm LED</span><span class="sxs-lookup"><span data-stu-id="d15ed-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="d15ed-124">Hallo Ethernet-kabel</span><span class="sxs-lookup"><span data-stu-id="d15ed-124">hello Ethernet cable</span></span>

![Dingen in uw starterskit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="d15ed-126">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="d15ed-126">You also need:</span></span>

* <span data-ttu-id="d15ed-127">Een bekabelde of draadloze verbinding voor Pi tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="d15ed-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="d15ed-128">Een USB-SD adapter of mini-SD-kaart tooburn Hallo OS-installatiekopie op Hallo microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="d15ed-128">A USB-SD adapter or mini-SD card tooburn hello OS image onto hello microSD card.</span></span>
* <span data-ttu-id="d15ed-129">Een computer met Windows, Mac of Linux.</span><span class="sxs-lookup"><span data-stu-id="d15ed-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="d15ed-130">Hallo-computer is gebruikte tooinstall Raspbian op Hallo microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="d15ed-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="d15ed-131">Een Internet verbinding toodownload Hallo benodigde hulpprogramma's en software.</span><span class="sxs-lookup"><span data-stu-id="d15ed-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="d15ed-132">Raspbian installeren op Hallo MicroSD-kaart</span><span class="sxs-lookup"><span data-stu-id="d15ed-132">Install Raspbian on hello MicroSD card</span></span>
<span data-ttu-id="d15ed-133">Hallo microSD-kaart voor de installatie van Hallo Raspbian afbeelding voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="d15ed-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="d15ed-134">Raspbian downloaden.</span><span class="sxs-lookup"><span data-stu-id="d15ed-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="d15ed-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) Hallo ZIP-bestand voor Raspbian Jessie met Pixel.</span><span class="sxs-lookup"><span data-stu-id="d15ed-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="d15ed-136">Pak Hallo Raspbian installatiekopie tooa map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d15ed-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="d15ed-137">Installeer Raspbian toohello microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="d15ed-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="d15ed-138">[Download](https://www.etcher.io) en Hallo Etcher SD-kaart brander hulpprogramma installeren.</span><span class="sxs-lookup"><span data-stu-id="d15ed-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="d15ed-139">Voer Etcher en Hallo Raspbian installatiekopie die u hebt opgehaald in stap 1.</span><span class="sxs-lookup"><span data-stu-id="d15ed-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="d15ed-140">Selecteer Hallo microSD-kaart station.</span><span class="sxs-lookup"><span data-stu-id="d15ed-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="d15ed-141">Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd Hallo juiste station.</span><span class="sxs-lookup"><span data-stu-id="d15ed-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="d15ed-142">Klik op **Flash** tooinstall Raspbian toohello microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="d15ed-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="d15ed-143">Hallo microSD-kaart van uw computer verwijderen wanneer de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="d15ed-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="d15ed-144">Het is veilig tooremove hello microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of Hallo microSD-kaart is voltooid ontkoppelt.</span><span class="sxs-lookup"><span data-stu-id="d15ed-144">It is safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="d15ed-145">Hallo microSD-kaart invoegen in uw Pi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-145">Insert hello microSD card into your Pi.</span></span>

![Plaats Hallo SD-kaart](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="d15ed-147">Pi inschakelen</span><span class="sxs-lookup"><span data-stu-id="d15ed-147">Turn on Pi</span></span>
<span data-ttu-id="d15ed-148">Pi inschakelen met behulp van Hallo micro USB-kabel en Hallo voeding.</span><span class="sxs-lookup"><span data-stu-id="d15ed-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Inschakelen](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="d15ed-150">Het is belangrijk toouse Hallo voeding in Hallo kit ten minste 2A toomake ervoor dat uw frambozen voldoende toowork power correct heeft.</span><span class="sxs-lookup"><span data-stu-id="d15ed-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="d15ed-151">SSH inschakelen</span><span class="sxs-lookup"><span data-stu-id="d15ed-151">Enable SSH</span></span>
<span data-ttu-id="d15ed-152">Vanaf de release van November 2016 Hallo heeft Raspbian Hallo SSH-server is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d15ed-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="d15ed-153">U moet tooenable deze handmatig.</span><span class="sxs-lookup"><span data-stu-id="d15ed-153">You need tooenable it manually.</span></span> <span data-ttu-id="d15ed-154">U kunt verwijzen toohello [officiële instructies](https://www.raspberrypi.org/documentation/remote-access/ssh/) of verbinding maken met een monitor en gaat u te**voorkeuren-frambozen Pi Configuration >** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="d15ed-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="d15ed-155">Frambozen Pi 3 toohello netwerk verbinden</span><span class="sxs-lookup"><span data-stu-id="d15ed-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="d15ed-156">U kunt Pi tooa bekabeld netwerk of tooa draadloze netwerk verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="d15ed-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="d15ed-157">Zorg ervoor dat Pi verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="d15ed-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="d15ed-158">U kunt bijvoorbeeld Pi toohello die dezelfde switch dat uw computer is verbonden met verbinden.</span><span class="sxs-lookup"><span data-stu-id="d15ed-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="d15ed-159">Verbinding maken met tooa bekabelde netwerk</span><span class="sxs-lookup"><span data-stu-id="d15ed-159">Connect tooa wired network</span></span>
<span data-ttu-id="d15ed-160">Gebruik Hallo Ethernet-kabel tooconnect Pi tooyour bekabelde netwerk.</span><span class="sxs-lookup"><span data-stu-id="d15ed-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="d15ed-161">Hallo inschakelen twee LED's op Pi als Hallo-verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="d15ed-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Verbinding maken met behulp van een Ethernet-kabel](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="d15ed-163">Verbinding maken met het draadloze netwerk tooa</span><span class="sxs-lookup"><span data-stu-id="d15ed-163">Connect tooa wireless network</span></span>
<span data-ttu-id="d15ed-164">Ga als volgt Hallo [instructies](https://www.raspberrypi.org/learning/software-guide/wifi/) van Hallo frambozen Pi Foundation tooconnect Pi tooyour draadloos netwerk.</span><span class="sxs-lookup"><span data-stu-id="d15ed-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="d15ed-165">Deze instructies, moet u toofirst verbinding maken met een monitor en een toetsenbord tooPi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="d15ed-166">Hallo LED tooPi verbinding</span><span class="sxs-lookup"><span data-stu-id="d15ed-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="d15ed-167">toocomplete deze taak, gebruik Hallo [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), connector kabels Hallo Hallo LED en Hallo weerstand.</span><span class="sxs-lookup"><span data-stu-id="d15ed-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="d15ed-168">Verbind ze toohello [voor algemene doeleinden input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO)-poorten van Pi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard LED en weerstand](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="d15ed-170">Hallo korter arm van Hallo LED te verbinden**GPIO GND (pincode 6)**.</span><span class="sxs-lookup"><span data-stu-id="d15ed-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="d15ed-171">Verbinding maken met Hallo langer arm van Hallo LED tooone arm van Hallo weerstand.</span><span class="sxs-lookup"><span data-stu-id="d15ed-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="d15ed-172">Verbinding maken met andere arm van Hallo weerstand te Hallo**GPIO 4 (7 pincode)**.</span><span class="sxs-lookup"><span data-stu-id="d15ed-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="d15ed-173">Houd er rekening mee dat Hallo LED polariteit belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="d15ed-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="d15ed-174">Deze instelling polariteit staat bekend als actief laag.</span><span class="sxs-lookup"><span data-stu-id="d15ed-174">This polarity setting is commonly known as Active Low.</span></span>

![Pin-out](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="d15ed-176">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="d15ed-176">Congratulations!</span></span> <span data-ttu-id="d15ed-177">U hebt geconfigureerd Pi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="d15ed-178">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d15ed-178">Summary</span></span>
<span data-ttu-id="d15ed-179">In dit artikel hebt u geleerd hoe tooconfigure door Raspbian, verbindende Pi tooa netwerk, installeren en verbinding maken met een tooPi LED Pi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="d15ed-180">Houd er rekening mee dat Hallo die LED nog niet branden.</span><span class="sxs-lookup"><span data-stu-id="d15ed-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="d15ed-181">de volgende taak Hallo is tooinstall Hallo vereiste hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="d15ed-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Hardware is gereed](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="d15ed-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d15ed-183">Next steps</span></span>
[<span data-ttu-id="d15ed-184">Hallo-hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="d15ed-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

