---
title: 'Connect Intel Edison (C) tooAzure IoT - les 1: apparaat configureren | Microsoft Docs'
description: Intel Edison configureren voor het eerste gebruik.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino instellen, verbinding arduino toopc, setup arduino, arduino mededelingenbord
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
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="94a8c-104">Uw Edison Intel configureren</span><span class="sxs-lookup"><span data-stu-id="94a8c-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="94a8c-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="94a8c-105">What you will do</span></span>
<span data-ttu-id="94a8c-106">Intel Edison configureren voor gebruik van de eerste keer door montage Hallo mededelingenbord, het opstarten van en configuratie hulpprogramma tooyour bureaublad OS tooflash installeren van Edison firmware, instellen van het wachtwoord in en sluit het tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="94a8c-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="94a8c-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="94a8c-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="94a8c-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="94a8c-108">What you will learn</span></span>
<span data-ttu-id="94a8c-109">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="94a8c-109">In this article, you will learn:</span></span>

* <span data-ttu-id="94a8c-110">Hoe tooassemble Edison board en inschakelen van.</span><span class="sxs-lookup"><span data-stu-id="94a8c-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="94a8c-111">Hoe tooflash Edison van firmware, wachtwoord instellen en Wi-Fi-verbinding.</span><span class="sxs-lookup"><span data-stu-id="94a8c-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="94a8c-112">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="94a8c-112">What you need</span></span>
<span data-ttu-id="94a8c-113">toocomplete deze bewerking moet u volgende onderdelen met de Intel Edison Starter Kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="94a8c-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="94a8c-114">Intel® Edison-module</span><span class="sxs-lookup"><span data-stu-id="94a8c-114">Intel® Edison module</span></span>
* <span data-ttu-id="94a8c-115">Arduino uitbreiding mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="94a8c-115">Arduino expansion board</span></span>
* <span data-ttu-id="94a8c-116">Een tussenruimte balken of schroeven in Hallo verpakking, met inbegrip van twee schroeven toofasten Hallo module toohello uitbreiding mededelingenbord en vier sets schroeven en plastic spacers meegeleverd.</span><span class="sxs-lookup"><span data-stu-id="94a8c-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="94a8c-117">Een tooType Micro B een USB-kabel</span><span class="sxs-lookup"><span data-stu-id="94a8c-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="94a8c-118">Een voeding direct huidige (DC).</span><span class="sxs-lookup"><span data-stu-id="94a8c-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="94a8c-119">Het prioriteitsniveau van uw voeding moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="94a8c-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="94a8c-120">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="94a8c-120">7-15V DC</span></span>
  - <span data-ttu-id="94a8c-121">Ten minste 1500mA</span><span class="sxs-lookup"><span data-stu-id="94a8c-121">At least 1500mA</span></span>
  - <span data-ttu-id="94a8c-122">Hallo center/interne pincode moet Hallo positieve pool van Hallo-voeding</span><span class="sxs-lookup"><span data-stu-id="94a8c-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Dingen in uw starterskit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="94a8c-124">U hebt ook het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="94a8c-124">You also need:</span></span>

* <span data-ttu-id="94a8c-125">Een computer met Windows, Mac of Linux.</span><span class="sxs-lookup"><span data-stu-id="94a8c-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="94a8c-126">Een draadloze verbinding voor Edison tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="94a8c-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="94a8c-127">Een Internet verbinding toodownload configuratiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="94a8c-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="94a8c-128">Het mededelingenbord samenstellen</span><span class="sxs-lookup"><span data-stu-id="94a8c-128">Assemble your board</span></span>

<span data-ttu-id="94a8c-129">Deze sectie bevat stappen tooattach het mededelingenbord Intel® Edison module tooyour uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="94a8c-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="94a8c-130">Hallo Intel® Edison module binnen Hallo wit overzicht op het mededelingenbord uitbreiding, Hallo gaten op Hallo-module met Hallo schroeven op Hallo uitbreiding mededelingenbord uitgelijnd plaatsen.</span><span class="sxs-lookup"><span data-stu-id="94a8c-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="94a8c-131">Druk op Hallo module onder Hallo woorden `What will you make?` totdat u denkt een module dat.</span><span class="sxs-lookup"><span data-stu-id="94a8c-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="94a8c-133">Hallo twee hexadecimale nuts (opgenomen in het Hallo-pakket) toosecure Hallo module toohello uitbreiding mededelingenbord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="94a8c-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="94a8c-135">Een installatie in een van de vier hoek gaten op Hallo uitbreiding mededelingenbord Hallo invoegen.</span><span class="sxs-lookup"><span data-stu-id="94a8c-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="94a8c-136">Draai en dat een witte Hallo plastic spacers op Hallo-installatie wordt versterkt.</span><span class="sxs-lookup"><span data-stu-id="94a8c-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="94a8c-138">Herhaal dit voor Hallo andere spacers drie hoek.</span><span class="sxs-lookup"><span data-stu-id="94a8c-138">Repeat for hello other three corner spacers.</span></span>

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="94a8c-140">Nu is het mededelingenbord samengesteld.</span><span class="sxs-lookup"><span data-stu-id="94a8c-140">Now your board is assembled.</span></span>

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="94a8c-142">Geef Edison</span><span class="sxs-lookup"><span data-stu-id="94a8c-142">Power up Edison</span></span>

1. <span data-ttu-id="94a8c-143">Hallo-voeding sluit.</span><span class="sxs-lookup"><span data-stu-id="94a8c-143">Plug in hello power supply.</span></span>

   ![Plug-in-voeding](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="94a8c-145">Een groene LED (met de naam DS1 op Hallo Arduino * uitbreiding mededelingenbord) moet branden en blijf branden.</span><span class="sxs-lookup"><span data-stu-id="94a8c-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="94a8c-146">Wacht een minuut voor Hallo mededelingenbord toofinish-up wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="94a8c-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="94a8c-147">Als u een DC-voeding niet hebt, kunt u nog steeds power Hallo mededelingenbord via een USB-poort.</span><span class="sxs-lookup"><span data-stu-id="94a8c-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="94a8c-148">Zie `Connect Edison tooyour computer` sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="94a8c-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="94a8c-149">Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.</span><span class="sxs-lookup"><span data-stu-id="94a8c-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="94a8c-150">Verbind Edison tooyour computer</span><span class="sxs-lookup"><span data-stu-id="94a8c-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="94a8c-151">Schakelen naar beneden Hallo microswitch naar Hallo twee micro USB-poorten, zodat Edison in de apparaatmodus.</span><span class="sxs-lookup"><span data-stu-id="94a8c-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="94a8c-152">Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="94a8c-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Omlaag Hallo microswitch in-of uitschakelen](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="94a8c-154">Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="94a8c-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="94a8c-156">Plug Hallo andere einde van USB-kabel op uw computer.</span><span class="sxs-lookup"><span data-stu-id="94a8c-156">Plug hello other end of USB cable into your computer.</span></span>

   ![Computer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="94a8c-158">Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).</span><span class="sxs-lookup"><span data-stu-id="94a8c-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="94a8c-159">Downloaden en uitvoeren van hulpprogramma voor serverconfiguratie Hallo</span><span class="sxs-lookup"><span data-stu-id="94a8c-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="94a8c-160">Ophalen van de nieuwste configuratiehulpprogramma Hallo van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld onder Hallo `Installers` kop.</span><span class="sxs-lookup"><span data-stu-id="94a8c-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="94a8c-161">Hallo-hulpprogramma uitvoeren en volg de op het scherm te klikken naast waar nodig-instructies</span><span class="sxs-lookup"><span data-stu-id="94a8c-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="94a8c-162">Flash-firmware</span><span class="sxs-lookup"><span data-stu-id="94a8c-162">Flash firmware</span></span>
1. <span data-ttu-id="94a8c-163">Op Hallo `Set up options` pagina, klikt u op `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="94a8c-164">Selecteer Hallo installatiekopie tooflash op het mededelingenbord op een van de volgende Hallo manieren:</span><span class="sxs-lookup"><span data-stu-id="94a8c-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="94a8c-165">toodownload en flash het mededelingenbord met Hallo meest recente firmware installatiekopie beschikbaar van Intel, selecteer `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="94a8c-166">het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, selecteert u tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="94a8c-167">Tooand Selecteer Hallo afbeelding u tooflash tooyour mededelingenbord wilt doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="94a8c-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="94a8c-168">hulpprogramma voor Hallo setup probeert tooflash het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="94a8c-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="94a8c-169">Hallo hele knipperende proces kan too10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="94a8c-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="94a8c-170">Wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="94a8c-170">Set password</span></span>
1. <span data-ttu-id="94a8c-171">Op Hallo `Set up options` pagina, klikt u op `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="94a8c-172">U kunt een aangepaste naam voor uw kaart Intel® Edison instellen.</span><span class="sxs-lookup"><span data-stu-id="94a8c-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="94a8c-173">Dit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="94a8c-173">This is optional.</span></span>
3. <span data-ttu-id="94a8c-174">Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="94a8c-175">Markeer omlaag Hallo-wachtwoord wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="94a8c-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="94a8c-176">Wi-Fi-verbinding</span><span class="sxs-lookup"><span data-stu-id="94a8c-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="94a8c-177">Op Hallo `Set up options` pagina, klikt u op `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="94a8c-178">Wacht up tooone minuut als uw computer scans voor Wi-Fi-netwerken beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="94a8c-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="94a8c-179">Van Hallo `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="94a8c-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="94a8c-180">Van Hallo `Security` vervolgkeuzelijst, selecteer Hallo-netwerk beveiligingstype.</span><span class="sxs-lookup"><span data-stu-id="94a8c-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="94a8c-181">Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="94a8c-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="94a8c-182">Markeer omlaag Hallo IP-adres, wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="94a8c-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="94a8c-183">Zorg ervoor dat Edison verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="94a8c-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="94a8c-184">Uw computer verbinding maakt tooyour Edison met Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="94a8c-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="94a8c-185">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="94a8c-185">Congratulations!</span></span> <span data-ttu-id="94a8c-186">U hebt Edison geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="94a8c-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="94a8c-187">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="94a8c-187">Summary</span></span>
<span data-ttu-id="94a8c-188">In dit artikel hebt geleerd hoe tooassemble Edison mededelingenbord Hallo, flash de firmware, setup wachtwoord en verbindt u deze tooWi-Fi met behulp van hulpprogramma voor serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="94a8c-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="94a8c-189">Houd er rekening mee dat Hallo die LED nog niet branden.</span><span class="sxs-lookup"><span data-stu-id="94a8c-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="94a8c-190">de volgende taak Hallo is tooinstall Hallo vereiste hulpprogramma's en software in voorbereiding voor het uitvoeren van een voorbeeld van toepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="94a8c-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94a8c-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94a8c-191">Next steps</span></span>
<span data-ttu-id="94a8c-192">[Hallo-hulpprogramma's ophalen][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="94a8c-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md