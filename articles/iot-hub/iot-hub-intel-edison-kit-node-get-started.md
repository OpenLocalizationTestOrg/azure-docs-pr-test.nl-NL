---
title: aaaIntel Edison toocloud (Node.js) - verbinding maken met Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met Intel Edison tooAzure IoT Hub voor Intel Edison toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel edison iothub, intel edison verzenden gegevens toocloud, intel edison toocloud
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="b7543-104">Verbinding maken met Intel Edison tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="b7543-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="b7543-105">In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met Intel Edison leren.</span><span class="sxs-lookup"><span data-stu-id="b7543-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="b7543-106">U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="b7543-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="b7543-107">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="b7543-107">Don't have a kit yet?</span></span> <span data-ttu-id="b7543-108">Start [hier](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="b7543-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b7543-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="b7543-109">What you do</span></span>

* <span data-ttu-id="b7543-110">Intel Edison instellen en en Groove modules.</span><span class="sxs-lookup"><span data-stu-id="b7543-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="b7543-111">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="b7543-111">Create an IoT hub.</span></span>
* <span data-ttu-id="b7543-112">Een apparaat registreren voor Edison in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b7543-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="b7543-113">Een voorbeeld van een toepassing uitvoeren op Edison toosend sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="b7543-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="b7543-114">Verbinding maken met een Intel Edison tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="b7543-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="b7543-115">Vervolgens voert u een voorbeeld van toepassing op Edison toocollect temperatuur en vochtigheid gegevens uit een temperatuursensor Groove.</span><span class="sxs-lookup"><span data-stu-id="b7543-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="b7543-116">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="b7543-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b7543-117">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="b7543-117">What you learn</span></span>

* <span data-ttu-id="b7543-118">Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="b7543-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="b7543-119">Hoe tooconnect Edison met een temperatuursensor Groove.</span><span class="sxs-lookup"><span data-stu-id="b7543-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="b7543-120">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Edison.</span><span class="sxs-lookup"><span data-stu-id="b7543-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="b7543-121">Hoe toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b7543-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b7543-122">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="b7543-122">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="b7543-124">Hallo Intel Edison mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="b7543-124">hello Intel Edison board</span></span>
* <span data-ttu-id="b7543-125">Arduino uitbreiding mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="b7543-125">Arduino expansion board</span></span>
* <span data-ttu-id="b7543-126">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b7543-126">An active Azure subscription.</span></span> <span data-ttu-id="b7543-127">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="b7543-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b7543-128">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b7543-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="b7543-129">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="b7543-129">An Internet connection.</span></span>
* <span data-ttu-id="b7543-130">Een tooType Micro B een USB-kabel</span><span class="sxs-lookup"><span data-stu-id="b7543-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="b7543-131">Een voeding direct huidige (DC).</span><span class="sxs-lookup"><span data-stu-id="b7543-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="b7543-132">Het prioriteitsniveau van uw voeding moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="b7543-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="b7543-133">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="b7543-133">7-15V DC</span></span>
  - <span data-ttu-id="b7543-134">Ten minste 1500mA</span><span class="sxs-lookup"><span data-stu-id="b7543-134">At least 1500mA</span></span>
  - <span data-ttu-id="b7543-135">Hallo center/interne pincode moet Hallo positieve pool van Hallo-voeding</span><span class="sxs-lookup"><span data-stu-id="b7543-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="b7543-136">Hallo volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="b7543-136">hello following items are optional:</span></span>

* <span data-ttu-id="b7543-137">Groove Base schild V2</span><span class="sxs-lookup"><span data-stu-id="b7543-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="b7543-138">Groove - temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="b7543-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="b7543-139">Groove-kabel</span><span class="sxs-lookup"><span data-stu-id="b7543-139">Grove Cable</span></span>
* <span data-ttu-id="b7543-140">Een tussenruimte balken of schroeven in Hallo verpakking, met inbegrip van twee schroeven toofasten Hallo module toohello uitbreiding mededelingenbord en vier sets schroeven en plastic spacers meegeleverd.</span><span class="sxs-lookup"><span data-stu-id="b7543-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="b7543-141">Deze items zijn optioneel, omdat Hallo code voorbeeld ondersteuning sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="b7543-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="b7543-142">Intel Edison instellen</span><span class="sxs-lookup"><span data-stu-id="b7543-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="b7543-143">Het mededelingenbord samenstellen</span><span class="sxs-lookup"><span data-stu-id="b7543-143">Assemble your board</span></span>

<span data-ttu-id="b7543-144">Deze sectie bevat stappen tooattach het mededelingenbord Intel® Edison module tooyour uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="b7543-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="b7543-145">Hallo Intel® Edison module binnen Hallo wit overzicht op het mededelingenbord uitbreiding, Hallo gaten op Hallo-module met Hallo schroeven op Hallo uitbreiding mededelingenbord uitgelijnd plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b7543-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="b7543-146">Druk op Hallo module onder Hallo woorden `What will you make?` totdat u denkt een module dat.</span><span class="sxs-lookup"><span data-stu-id="b7543-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="b7543-148">Hallo twee hexadecimale nuts (opgenomen in het Hallo-pakket) toosecure Hallo module toohello uitbreiding mededelingenbord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b7543-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="b7543-150">Een installatie in een van de vier hoek gaten op Hallo uitbreiding mededelingenbord Hallo invoegen.</span><span class="sxs-lookup"><span data-stu-id="b7543-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="b7543-151">Draai en dat een witte Hallo plastic spacers op Hallo-installatie wordt versterkt.</span><span class="sxs-lookup"><span data-stu-id="b7543-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="b7543-153">Herhaal dit voor Hallo andere spacers drie hoek.</span><span class="sxs-lookup"><span data-stu-id="b7543-153">Repeat for hello other three corner spacers.</span></span>

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="b7543-155">Nu is het mededelingenbord samengesteld.</span><span class="sxs-lookup"><span data-stu-id="b7543-155">Now your board is assembled.</span></span>

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="b7543-157">Verbinding maken met de Hallo Groove Base schild en Hallo-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="b7543-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="b7543-158">Hallo Groove Base schild op het mededelingenbord tooyour plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b7543-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="b7543-159">Zorg ervoor dat alle pincodes goed zijn aangesloten op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="b7543-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Groove Base schild](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="b7543-161">Gebruik Groove kabel tooconnect Groove-temperatuursensor op Hallo Groove Base schild **A0** poort.</span><span class="sxs-lookup"><span data-stu-id="b7543-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Verbinding maken met tootemperature-temperatuursensor](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison en sensor verbinding](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="b7543-164">Nu is uw sensor gereed.</span><span class="sxs-lookup"><span data-stu-id="b7543-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="b7543-165">Geef Edison</span><span class="sxs-lookup"><span data-stu-id="b7543-165">Power up Edison</span></span>

1. <span data-ttu-id="b7543-166">Hallo-voeding sluit.</span><span class="sxs-lookup"><span data-stu-id="b7543-166">Plug in hello power supply.</span></span>

   ![Plug-in-voeding](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="b7543-168">Een groene LED (met de naam DS1 op Hallo Arduino * uitbreiding mededelingenbord) moet branden en blijf branden.</span><span class="sxs-lookup"><span data-stu-id="b7543-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="b7543-169">Wacht een minuut voor Hallo mededelingenbord toofinish-up wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="b7543-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b7543-170">Als u een DC-voeding niet hebt, kunt u nog steeds power Hallo mededelingenbord via een USB-poort.</span><span class="sxs-lookup"><span data-stu-id="b7543-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="b7543-171">Zie `Connect Edison tooyour computer` sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b7543-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="b7543-172">Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.</span><span class="sxs-lookup"><span data-stu-id="b7543-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="b7543-173">Verbind Edison tooyour computer</span><span class="sxs-lookup"><span data-stu-id="b7543-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="b7543-174">Schakelen naar beneden Hallo microswitch naar Hallo twee micro USB-poorten, zodat Edison in de apparaatmodus.</span><span class="sxs-lookup"><span data-stu-id="b7543-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="b7543-175">Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="b7543-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Omlaag Hallo microswitch in-of uitschakelen](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="b7543-177">Hallo micro USB-kabel aansluiten op Hallo bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="b7543-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="b7543-179">Plug Hallo andere einde van USB-kabel op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b7543-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Computer USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="b7543-181">Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).</span><span class="sxs-lookup"><span data-stu-id="b7543-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="b7543-182">Downloaden en uitvoeren van hulpprogramma voor serverconfiguratie Hallo</span><span class="sxs-lookup"><span data-stu-id="b7543-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="b7543-183">Ophalen van de nieuwste configuratiehulpprogramma Hallo van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld onder Hallo `Installers` kop.</span><span class="sxs-lookup"><span data-stu-id="b7543-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="b7543-184">Hallo-hulpprogramma uitvoeren en volg de op het scherm te klikken naast waar nodig-instructies</span><span class="sxs-lookup"><span data-stu-id="b7543-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="b7543-185">Flash-firmware</span><span class="sxs-lookup"><span data-stu-id="b7543-185">Flash firmware</span></span>
1. <span data-ttu-id="b7543-186">Op Hallo `Set up options` pagina, klikt u op `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="b7543-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="b7543-187">Selecteer Hallo installatiekopie tooflash op het mededelingenbord op een van de volgende Hallo manieren:</span><span class="sxs-lookup"><span data-stu-id="b7543-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="b7543-188">toodownload en flash het mededelingenbord met Hallo meest recente firmware installatiekopie beschikbaar van Intel, selecteer `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="b7543-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="b7543-189">het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, selecteert u tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="b7543-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="b7543-190">Tooand Selecteer Hallo afbeelding u tooflash tooyour mededelingenbord wilt doorzoeken.</span><span class="sxs-lookup"><span data-stu-id="b7543-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="b7543-191">hulpprogramma voor Hallo setup probeert tooflash het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="b7543-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="b7543-192">Hallo hele knipperende proces kan too10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="b7543-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="b7543-193">Wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="b7543-193">Set password</span></span>
1. <span data-ttu-id="b7543-194">Op Hallo `Set up options` pagina, klikt u op `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="b7543-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="b7543-195">U kunt een aangepaste naam voor uw kaart Intel® Edison instellen.</span><span class="sxs-lookup"><span data-stu-id="b7543-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="b7543-196">Dit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="b7543-196">This is optional.</span></span>
3. <span data-ttu-id="b7543-197">Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.</span><span class="sxs-lookup"><span data-stu-id="b7543-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="b7543-198">Markeer omlaag Hallo-wachtwoord wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7543-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="b7543-199">Wi-Fi-verbinding</span><span class="sxs-lookup"><span data-stu-id="b7543-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="b7543-200">Op Hallo `Set up options` pagina, klikt u op `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="b7543-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="b7543-201">Wacht up tooone minuut als uw computer scans voor Wi-Fi-netwerken beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b7543-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="b7543-202">Van Hallo `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="b7543-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="b7543-203">Van Hallo `Security` vervolgkeuzelijst, selecteer Hallo-netwerk beveiligingstype.</span><span class="sxs-lookup"><span data-stu-id="b7543-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="b7543-204">Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="b7543-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="b7543-205">Markeer omlaag Hallo IP-adres, wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7543-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="b7543-206">Zorg ervoor dat Edison verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="b7543-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="b7543-207">Uw computer verbinding maakt tooyour Edison met Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b7543-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Verbinding maken met tootemperature-temperatuursensor](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="b7543-209">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="b7543-209">Congratulations!</span></span> <span data-ttu-id="b7543-210">U hebt Edison geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b7543-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="b7543-211">Een voorbeeld van een toepassing uitvoeren op Intel Edison</span><span class="sxs-lookup"><span data-stu-id="b7543-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="b7543-212">Hallo-SDK van Azure IoT-apparaat voorbereiden</span><span class="sxs-lookup"><span data-stu-id="b7543-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="b7543-213">Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour Intel Edison Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7543-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="b7543-214">Hallo IP-adres is van het hulpprogramma voor serverconfiguratie Hallo en Hallo wachtwoord Hallo een die u hebt ingesteld in dat hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="b7543-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="b7543-215">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="b7543-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="b7543-216">Hallo ingebouwde SSH-client op Ubuntu- of Mac OS.</span><span class="sxs-lookup"><span data-stu-id="b7543-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="b7543-217">Kloon Hallo voorbeeld-app tooyour clientapparaat.</span><span class="sxs-lookup"><span data-stu-id="b7543-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="b7543-218">Navigeer toohello opslagplaats map toorun Hallo opdracht tooinstall na alle pakketten, toocomplete van serval minuten kan duren.</span><span class="sxs-lookup"><span data-stu-id="b7543-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="b7543-219">Configureren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="b7543-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="b7543-220">Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="b7543-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Configuratiebestand](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="b7543-222">Er zijn twee macro's in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="b7543-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="b7543-223">Hallo eerst een is `INTERVAL`, definieert een Hallo tijdsinterval tussen twee berichten die toocloud verzenden.</span><span class="sxs-lookup"><span data-stu-id="b7543-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="b7543-224">tweede Hallo `simulatedData`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="b7543-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="b7543-225">Als u **geen Hallo sensor**stelt hello `simulatedData` waarde te`true` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b7543-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="b7543-226">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="b7543-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="b7543-227">Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b7543-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="b7543-228">Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="b7543-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="b7543-229">U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="b7543-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Output - sensorgegevens uit Intel Edison tooyour iothub worden verzonden](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="b7543-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b7543-231">Next steps</span></span>

<span data-ttu-id="b7543-232">U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b7543-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
