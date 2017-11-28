---
title: 'Connect Intel Edison (C) naar Azure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Intel Edison configureren voor het eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding maken met arduino pc, setup arduino, arduino mededelingenbord
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="c8436-104">Uw Edison Intel configureren</span><span class="sxs-lookup"><span data-stu-id="c8436-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c8436-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="c8436-105">What you will do</span></span>
<span data-ttu-id="c8436-106">Intel Edison configureren voor het eerste gebruik door de bestuur, het opstarten van montage en configuration tool installeren op uw bureaublad besturingssysteem naar flash Edison van firmware, stel het wachtwoord en verbinding met Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c8436-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="c8436-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c8436-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c8436-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="c8436-108">What you will learn</span></span>
<span data-ttu-id="c8436-109">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="c8436-109">In this article, you will learn:</span></span>

* <span data-ttu-id="c8436-110">Informatie over het samenstellen van Edison mededelingenbord en inschakelen van.</span><span class="sxs-lookup"><span data-stu-id="c8436-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="c8436-111">Het flash Edison van firmware, wachtwoord instellen en Wi-Fi-verbinding.</span><span class="sxs-lookup"><span data-stu-id="c8436-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c8436-112">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="c8436-112">What you need</span></span>
<span data-ttu-id="c8436-113">Om deze bewerking niet voltooien, moet u de volgende onderdelen met de Intel Edison Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="c8436-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="c8436-114">Intel® Edison-module</span><span class="sxs-lookup"><span data-stu-id="c8436-114">Intel® Edison module</span></span>
* <span data-ttu-id="c8436-115">Arduino uitbreiding mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="c8436-115">Arduino expansion board</span></span>
* <span data-ttu-id="c8436-116">Een tussenruimte balken of schroeven opgenomen in de verpakking, met inbegrip van twee schroeven om de module aan de bestuur uitbreiding en vier sets schroeven en plastic spacers bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c8436-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="c8436-117">Een B Micro van Type A USB-kabel</span><span class="sxs-lookup"><span data-stu-id="c8436-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="c8436-118">Een voeding direct huidige (DC).</span><span class="sxs-lookup"><span data-stu-id="c8436-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="c8436-119">Het prioriteitsniveau van uw voeding moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="c8436-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="c8436-120">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="c8436-120">7-15V DC</span></span>
  - <span data-ttu-id="c8436-121">Ten minste 1500mA</span><span class="sxs-lookup"><span data-stu-id="c8436-121">At least 1500mA</span></span>
  - <span data-ttu-id="c8436-122">De pincode center/interne moet de positieve pool van de voeding</span><span class="sxs-lookup"><span data-stu-id="c8436-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Dingen in uw starterskit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="c8436-124">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="c8436-124">You also need:</span></span>

* <span data-ttu-id="c8436-125">Een computer met Windows, Mac of Linux.</span><span class="sxs-lookup"><span data-stu-id="c8436-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="c8436-126">Een draadloze verbinding voor Edison verbinding maken met.</span><span class="sxs-lookup"><span data-stu-id="c8436-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="c8436-127">Een internetverbinding beschikken om het downloaden van hulpprogramma voor serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="c8436-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="c8436-128">Het mededelingenbord samenstellen</span><span class="sxs-lookup"><span data-stu-id="c8436-128">Assemble your board</span></span>

<span data-ttu-id="c8436-129">Deze sectie bevat stappen om uw module Intel® Edison koppelen aan het mededelingenbord uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="c8436-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="c8436-130">Plaats de Intel® Edison module binnen het wit overzicht op het mededelingenbord uitbreiding uitgelijnd in de gaten in de module met de schroeven op het mededelingenbord van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="c8436-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="c8436-131">Druk op de module onder de woorden `What will you make?` totdat u denkt een module dat.</span><span class="sxs-lookup"><span data-stu-id="c8436-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="c8436-133">De twee hexadecimale nuts (opgenomen in het pakket) gebruiken voor het beveiligen van de module in op het mededelingenbord van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="c8436-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="c8436-135">Voeg een installatie in een van de vier hoek gaten op het mededelingenbord van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="c8436-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="c8436-136">Draai en dat een van de witte plastic spacers op de installatie wordt versterkt.</span><span class="sxs-lookup"><span data-stu-id="c8436-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="c8436-138">Herhaal voor de andere drie hoek spacers.</span><span class="sxs-lookup"><span data-stu-id="c8436-138">Repeat for the other three corner spacers.</span></span>

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="c8436-140">Nu is het mededelingenbord samengesteld.</span><span class="sxs-lookup"><span data-stu-id="c8436-140">Now your board is assembled.</span></span>

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="c8436-142">Geef Edison</span><span class="sxs-lookup"><span data-stu-id="c8436-142">Power up Edison</span></span>

1. <span data-ttu-id="c8436-143">Sluit de voeding.</span><span class="sxs-lookup"><span data-stu-id="c8436-143">Plug in the power supply.</span></span>

   ![Plug-in-voeding](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="c8436-145">Een groene LED (met de naam DS1 op het mededelingenbord Arduino * uitbreiding) moet branden en blijf branden.</span><span class="sxs-lookup"><span data-stu-id="c8436-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="c8436-146">Wacht een minuut voor de kaart te voltooien wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="c8436-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c8436-147">Als u een DC-voeding niet hebt, kunt u nog steeds het mededelingenbord via een USB-poort voor energiebeheer.</span><span class="sxs-lookup"><span data-stu-id="c8436-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="c8436-148">Zie `Connect Edison to your computer` sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c8436-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="c8436-149">Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.</span><span class="sxs-lookup"><span data-stu-id="c8436-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="c8436-150">Edison aansluiten op uw computer</span><span class="sxs-lookup"><span data-stu-id="c8436-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="c8436-151">Schakelen naar beneden de microswitch naar de twee micro USB-poorten, zodat Edison in de apparaatmodus.</span><span class="sxs-lookup"><span data-stu-id="c8436-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="c8436-152">Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="c8436-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Uitschakelen van de microswitch](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="c8436-154">De micro USB-kabel aansluiten op de bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="c8436-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="c8436-156">Het andere einde van USB-kabel aansluiten op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c8436-156">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="c8436-158">Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).</span><span class="sxs-lookup"><span data-stu-id="c8436-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="c8436-159">Downloaden en uitvoeren van het configuratiehulpprogramma</span><span class="sxs-lookup"><span data-stu-id="c8436-159">Download and run the configuration tool</span></span>
<span data-ttu-id="c8436-160">Ophalen van de nieuwste hulpprogramma voor serverconfiguratie van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld in de `Installers` kop.</span><span class="sxs-lookup"><span data-stu-id="c8436-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="c8436-161">Het hulpprogramma uitvoeren en volg de aanwijzingen op het scherm instructies en klik vervolgens op waar nodig</span><span class="sxs-lookup"><span data-stu-id="c8436-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="c8436-162">Flash-firmware</span><span class="sxs-lookup"><span data-stu-id="c8436-162">Flash firmware</span></span>
1. <span data-ttu-id="c8436-163">Op de `Set up options` pagina, klikt u op `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="c8436-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="c8436-164">Selecteer de installatiekopie moet op het mededelingenbord flash op een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="c8436-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="c8436-165">Als u wilt downloaden en het mededelingenbord met de meest recente firmware-installatiekopie beschikbaar van Intel flash, selecteer `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="c8436-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="c8436-166">Selecteer Flash het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="c8436-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="c8436-167">Blader naar en selecteer de installatiekopie die u wilt flash op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="c8436-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="c8436-168">Het hulpprogramma setup probeert te flash het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="c8436-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="c8436-169">Het hele knipperende proces kan maximaal 10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="c8436-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="c8436-170">Wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="c8436-170">Set password</span></span>
1. <span data-ttu-id="c8436-171">Op de `Set up options` pagina, klikt u op `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="c8436-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="c8436-172">U kunt een aangepaste naam voor uw kaart Intel® Edison instellen.</span><span class="sxs-lookup"><span data-stu-id="c8436-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="c8436-173">Dit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c8436-173">This is optional.</span></span>
3. <span data-ttu-id="c8436-174">Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.</span><span class="sxs-lookup"><span data-stu-id="c8436-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="c8436-175">Markeert u het wachtwoord dat later wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c8436-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="c8436-176">Wi-Fi-verbinding</span><span class="sxs-lookup"><span data-stu-id="c8436-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="c8436-177">Op de `Set up options` pagina, klikt u op `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="c8436-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="c8436-178">Wacht maximaal één minuut als uw computer wordt gescand naar beschikbare Wi-Fi-netwerken.</span><span class="sxs-lookup"><span data-stu-id="c8436-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="c8436-179">Van de `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="c8436-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="c8436-180">Van de `Security` vervolgkeuzelijst Selecteer beveiligingstype van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="c8436-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="c8436-181">Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="c8436-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="c8436-182">Markeer de IP-adres, die later wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c8436-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="c8436-183">Zorg ervoor dat Edison is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="c8436-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="c8436-184">Uw computer verbinding maakt met uw Edison met behulp van het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c8436-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="c8436-185">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="c8436-185">Congratulations!</span></span> <span data-ttu-id="c8436-186">U hebt Edison geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c8436-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="c8436-187">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c8436-187">Summary</span></span>
<span data-ttu-id="c8436-188">In dit artikel hebt u geleerd hoe het mededelingenbord Edison samenstellen, flash de firmware, setup wachtwoord en verbinding met Wi-Fi met behulp van hulpprogramma voor serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="c8436-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="c8436-189">Houd er rekening mee dat de LED nog niet branden.</span><span class="sxs-lookup"><span data-stu-id="c8436-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="c8436-190">De volgende taak is het installeren van de benodigde hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="c8436-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8436-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8436-191">Next steps</span></span>
<span data-ttu-id="c8436-192">[Download de hulpprogramma 's][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="c8436-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md