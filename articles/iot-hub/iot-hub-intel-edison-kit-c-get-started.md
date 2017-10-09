---
title: aaaIntel Edison toocloud (C) - verbinding maken met Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met Intel Edison tooAzure IoT Hub voor Intel Edison toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel edison iothub, intel edison verzenden gegevens toocloud, intel edison toocloud
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a><span data-ttu-id="cb993-104">Verbinding maken met Intel Edison tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="cb993-104">Connect Intel Edison tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="cb993-105">In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met Intel Edison leren.</span><span class="sxs-lookup"><span data-stu-id="cb993-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="cb993-106">U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="cb993-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="cb993-107">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="cb993-107">Don't have a kit yet?</span></span> <span data-ttu-id="cb993-108">Start [hier](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="cb993-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cb993-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="cb993-109">What you do</span></span>

* <span data-ttu-id="cb993-110">Intel Edison instellen en en Groove modules.</span><span class="sxs-lookup"><span data-stu-id="cb993-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="cb993-111">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="cb993-111">Create an IoT hub.</span></span>
* <span data-ttu-id="cb993-112">Een apparaat registreren voor Edison in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cb993-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="cb993-113">Een voorbeeld van een toepassing uitvoeren op Edison toosend sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="cb993-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="cb993-114">Verbinding maken met een Intel Edison tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="cb993-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="cb993-115">Vervolgens voert u een voorbeeld van toepassing op Edison toocollect temperatuur en vochtigheid gegevens uit een temperatuursensor Groove.</span><span class="sxs-lookup"><span data-stu-id="cb993-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="cb993-116">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="cb993-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cb993-117">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="cb993-117">What you learn</span></span>

* <span data-ttu-id="cb993-118">Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="cb993-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="cb993-119">Hoe tooconnect Edison met een temperatuursensor Groove.</span><span class="sxs-lookup"><span data-stu-id="cb993-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="cb993-120">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="cb993-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="cb993-121">Hoe toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cb993-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cb993-122">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="cb993-122">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="cb993-124">Hallo Intel Edison mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="cb993-124">hello Intel Edison board</span></span>
* <span data-ttu-id="cb993-125">Arduino uitbreiding mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="cb993-125">Arduino expansion board</span></span>
* <span data-ttu-id="cb993-126">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cb993-126">An active Azure subscription.</span></span> <span data-ttu-id="cb993-127">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="cb993-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="cb993-128">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cb993-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="cb993-129">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="cb993-129">An Internet connection.</span></span>
* <span data-ttu-id="cb993-130">Een tooType Micro B een USB-kabel</span><span class="sxs-lookup"><span data-stu-id="cb993-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="cb993-131">Een voeding direct huidige (DC).</span><span class="sxs-lookup"><span data-stu-id="cb993-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="cb993-132">Het prioriteitsniveau van uw voeding moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="cb993-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="cb993-133">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="cb993-133">7-15V DC</span></span>
  - <span data-ttu-id="cb993-134">Ten minste 1500mA</span><span class="sxs-lookup"><span data-stu-id="cb993-134">At least 1500mA</span></span>
  - <span data-ttu-id="cb993-135">Hallo center/interne pincode moet Hallo positieve pool van Hallo-voeding</span><span class="sxs-lookup"><span data-stu-id="cb993-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="cb993-136">Hallo volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="cb993-136">hello following items are optional:</span></span>

* <span data-ttu-id="cb993-137">Groove Base schild V2</span><span class="sxs-lookup"><span data-stu-id="cb993-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="cb993-138">Groove - temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="cb993-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="cb993-139">Groove-kabel</span><span class="sxs-lookup"><span data-stu-id="cb993-139">Grove Cable</span></span>
* <span data-ttu-id="cb993-140">Een tussenruimte balken of schroeven in Hallo verpakking, met inbegrip van twee schroeven toofasten Hallo module toohello uitbreiding mededelingenbord en vier sets schroeven en plastic spacers meegeleverd.</span><span class="sxs-lookup"><span data-stu-id="cb993-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="cb993-141">Deze items zijn optioneel, omdat Hallo code voorbeeld ondersteuning sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="cb993-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="cb993-142">Intel Edison instellen</span><span class="sxs-lookup"><span data-stu-id="cb993-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="cb993-143">Het mededelingenbord samenstellen</span><span class="sxs-lookup"><span data-stu-id="cb993-143">Assemble your board</span></span>

<span data-ttu-id="cb993-144">Deze sectie bevat stappen tooattach het mededelingenbord Intel® Edison module tooyour uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="cb993-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="cb993-145">Hallo Intel® Edison module binnen Hallo wit overzicht op het mededelingenbord uitbreiding, Hallo gaten op Hallo-module met Hallo schroeven op Hallo uitbreiding mededelingenbord uitgelijnd plaatsen.</span><span class="sxs-lookup"><span data-stu-id="cb993-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="cb993-146">Druk op Hallo module onder Hallo woorden `What will you make?` totdat u denkt een module dat.</span><span class="sxs-lookup"><span data-stu-id="cb993-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="cb993-148">Hallo twee hexadecimale nuts (opgenomen in het Hallo-pakket) toosecure Hallo module toohello uitbreiding mededelingenbord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cb993-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="cb993-150">Een installatie in een van de vier hoek gaten op Hallo uitbreiding mededelingenbord Hallo invoegen.</span><span class="sxs-lookup"><span data-stu-id="cb993-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="cb993-151">Draai en dat een witte Hallo plastic spacers op Hallo-installatie wordt versterkt.</span><span class="sxs-lookup"><span data-stu-id="cb993-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="cb993-153">Herhaal dit voor Hallo andere spacers drie hoek.</span><span class="sxs-lookup"><span data-stu-id="cb993-153">Repeat for hello other three corner spacers.</span></span>

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="cb993-155">Nu is het mededelingenbord samengesteld.</span><span class="sxs-lookup"><span data-stu-id="cb993-155">Now your board is assembled.</span></span>

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="cb993-157">Verbinding maken met de Hallo Groove Base schild en Hallo-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="cb993-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="cb993-158">Hallo Groove Base schild op het mededelingenbord tooyour plaatsen.</span><span class="sxs-lookup"><span data-stu-id="cb993-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="cb993-159">Zorg ervoor dat alle pincodes goed zijn aangesloten op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="cb993-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Groove Base schild](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="cb993-161">Gebruik Groove kabel tooconnect Groove-temperatuursensor op Hallo Groove Base schild **A0** poort.</span><span class="sxs-lookup"><span data-stu-id="cb993-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Verbinding maken met tootemperature-temperatuursensor](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison en sensor verbinding](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="cb993-164">Nu is uw sensor gereed.</span><span class="sxs-lookup"><span data-stu-id="cb993-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="cb993-165">Geef Edison</span><span class="sxs-lookup"><span data-stu-id="cb993-165">Power up Edison</span></span>

1. <span data-ttu-id="cb993-166">Hallo-voeding sluit.</span><span class="sxs-lookup"><span data-stu-id="cb993-166">Plug in hello power supply.</span></span>

   ![Plug-in-voeding](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="cb993-168">Een groene LED (met de naam DS1 op Hallo Arduino * uitbreiding mededelingenbord) moet branden en blijf branden.</span><span class="sxs-lookup"><span data-stu-id="cb993-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="cb993-169">Wacht een minuut voor Hallo mededelingenbord toofinish-up wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="cb993-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb993-170">Als u een DC-voeding niet hebt, kunt u nog steeds power Hallo mededelingenbord via een USB-poort.</span><span class="sxs-lookup"><span data-stu-id="cb993-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="cb993-171">Zie `Connect Edison tooyour computer` sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cb993-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="cb993-172">Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.</span><span class="sxs-lookup"><span data-stu-id="cb993-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="cb993-173">Verbind Edison tooyour computer</span><span class="sxs-lookup"><span data-stu-id="cb993-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="cb993-174">Schakelen naar beneden Hallo microswitch naar Hallo twee micro USB-poorten, zodat Edison in de apparaatmodus.</span><span class="sxs-lookup"><span data-stu-id="cb993-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="cb993-175">Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="cb993-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Omlaag Hallo microswitch in-of uitschakelen](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="cb993-177">Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="cb993-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="cb993-179">Plug Hallo andere einde van USB-kabel op uw computer.</span><span class="sxs-lookup"><span data-stu-id="cb993-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Computer USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="cb993-181">Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).</span><span class="sxs-lookup"><span data-stu-id="cb993-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="cb993-182">Downloaden en uitvoeren van hulpprogramma voor serverconfiguratie Hallo</span><span class="sxs-lookup"><span data-stu-id="cb993-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="cb993-183">Ophalen van de nieuwste configuratiehulpprogramma Hallo van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld onder Hallo `Installers` kop.</span><span class="sxs-lookup"><span data-stu-id="cb993-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="cb993-184">Hallo-hulpprogramma uitvoeren en volg de op het scherm te klikken naast waar nodig-instructies</span><span class="sxs-lookup"><span data-stu-id="cb993-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="cb993-185">Flash-firmware</span><span class="sxs-lookup"><span data-stu-id="cb993-185">Flash firmware</span></span>
1. <span data-ttu-id="cb993-186">Op Hallo `Set up options` pagina, klikt u op `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="cb993-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="cb993-187">Selecteer Hallo installatiekopie tooflash op het mededelingenbord op een van de volgende Hallo manieren:</span><span class="sxs-lookup"><span data-stu-id="cb993-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="cb993-188">toodownload en flash het mededelingenbord met Hallo meest recente firmware installatiekopie beschikbaar van Intel, selecteer `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="cb993-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="cb993-189">het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, selecteert u tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="cb993-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="cb993-190">Tooand Selecteer Hallo afbeelding u tooflash tooyour mededelingenbord wilt doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="cb993-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="cb993-191">hulpprogramma voor Hallo setup probeert tooflash het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="cb993-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="cb993-192">Hallo hele knipperende proces kan too10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="cb993-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="cb993-193">Wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="cb993-193">Set password</span></span>
1. <span data-ttu-id="cb993-194">Op Hallo `Set up options` pagina, klikt u op `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="cb993-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="cb993-195">U kunt een aangepaste naam voor uw kaart Intel® Edison instellen.</span><span class="sxs-lookup"><span data-stu-id="cb993-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="cb993-196">Dit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="cb993-196">This is optional.</span></span>
3. <span data-ttu-id="cb993-197">Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.</span><span class="sxs-lookup"><span data-stu-id="cb993-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="cb993-198">Markeer omlaag Hallo-wachtwoord wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cb993-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="cb993-199">Wi-Fi-verbinding</span><span class="sxs-lookup"><span data-stu-id="cb993-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="cb993-200">Op Hallo `Set up options` pagina, klikt u op `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="cb993-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="cb993-201">Wacht up tooone minuut als uw computer scans voor Wi-Fi-netwerken beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="cb993-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="cb993-202">Van Hallo `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="cb993-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="cb993-203">Van Hallo `Security` vervolgkeuzelijst, selecteer Hallo-netwerk beveiligingstype.</span><span class="sxs-lookup"><span data-stu-id="cb993-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="cb993-204">Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="cb993-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="cb993-205">Markeer omlaag Hallo IP-adres, wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cb993-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="cb993-206">Zorg ervoor dat Edison verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="cb993-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="cb993-207">Uw computer verbinding maakt tooyour Edison met Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="cb993-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Verbinding maken met tootemperature-temperatuursensor](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="cb993-209">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="cb993-209">Congratulations!</span></span> <span data-ttu-id="cb993-210">U hebt Edison geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cb993-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="cb993-211">Een voorbeeld van een toepassing uitvoeren op Intel Edison</span><span class="sxs-lookup"><span data-stu-id="cb993-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="cb993-212">Hallo-SDK van Azure IoT-apparaat voorbereiden</span><span class="sxs-lookup"><span data-stu-id="cb993-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="cb993-213">Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour Intel Edison Hallo.</span><span class="sxs-lookup"><span data-stu-id="cb993-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="cb993-214">Hallo IP-adres is van het hulpprogramma voor serverconfiguratie Hallo en Hallo wachtwoord Hallo een die u hebt ingesteld in dat hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="cb993-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="cb993-215">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="cb993-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="cb993-216">Hallo ingebouwde SSH-client op Ubuntu- of Mac OS (uitvoeren `ssh root@"hello IP address"`).</span><span class="sxs-lookup"><span data-stu-id="cb993-216">hello built-in SSH client on Ubuntu or macOS (run `ssh root@"hello IP address"`).</span></span>

2. <span data-ttu-id="cb993-217">Kloon Hallo voorbeeld-app tooyour clientapparaat.</span><span class="sxs-lookup"><span data-stu-id="cb993-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="cb993-218">Navigeer toohello opslagplaats map toorun Hallo na de opdracht toobuild Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="cb993-218">Then navigate toohello repo folder toorun hello following command toobuild Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a><span data-ttu-id="cb993-219">Hallo-voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="cb993-219">Configure hello sample application</span></span>

1. <span data-ttu-id="cb993-220">Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="cb993-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Configuratiebestand](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="cb993-222">Er zijn twee macro's in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="cb993-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="cb993-223">Hallo eerst een is `INTERVAL`, definieert een Hallo tijdsinterval tussen twee berichten die toocloud verzenden.</span><span class="sxs-lookup"><span data-stu-id="cb993-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="cb993-224">tweede Hallo `SIMULATED_DATA`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="cb993-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="cb993-225">Als u **geen Hallo sensor**stelt hello `SIMULATED_DATA` waarde te`1` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cb993-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="cb993-226">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="cb993-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="cb993-227">Hallo voorbeeldtoepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cb993-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="cb993-228">Hallo-voorbeeldtoepassing bouwen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="cb993-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Uitvoer bouwen](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="cb993-230">Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="cb993-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="cb993-231">Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="cb993-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="cb993-232">U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="cb993-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Output - sensorgegevens uit Intel Edison tooyour iothub worden verzonden](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="cb993-234">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb993-234">Next steps</span></span>

<span data-ttu-id="cb993-235">U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="cb993-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
