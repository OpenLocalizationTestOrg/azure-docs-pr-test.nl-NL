---
title: Intel Edison naar cloud (C) - Intel Edison verbinding maken met Azure IoT Hub | Microsoft Docs
description: Informatie over het instellen en Intel Edison verbinden met Azure IoT Hub voor Intel Edison gegevens verzenden naar het Azure-cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel edison iothub, intel edison verzenden van gegevens naar de cloud, intel edison naar cloud
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: edbdbe0230f742cd7228f04a4a83c9bd567527e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-c"></a><span data-ttu-id="3a832-104">Verbinding maken met Intel Edison Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="3a832-104">Connect Intel Edison to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="3a832-105">In deze zelfstudie maakt beginnen u door te leren over het werken met Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="3a832-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="3a832-106">Vervolgens leert u hoe u uw apparaten probleemloos verbinding met de cloud via [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="3a832-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="3a832-107">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="3a832-107">Don't have a kit yet?</span></span> <span data-ttu-id="3a832-108">Start [hier](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="3a832-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3a832-109">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="3a832-109">What you do</span></span>

* <span data-ttu-id="3a832-110">Intel Edison instellen en en Groove modules.</span><span class="sxs-lookup"><span data-stu-id="3a832-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="3a832-111">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="3a832-111">Create an IoT hub.</span></span>
* <span data-ttu-id="3a832-112">Een apparaat registreren voor Edison in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3a832-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="3a832-113">Een voorbeeld van een toepassing uitvoeren op Edison sensorgegevens verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3a832-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="3a832-114">Verbinding maken met Intel Edison naar een IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="3a832-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="3a832-115">Vervolgens voert u een voorbeeld van toepassing op Edison temperatuur en vochtigheid gegevens te verzamelen van een temperatuursensor Groove.</span><span class="sxs-lookup"><span data-stu-id="3a832-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="3a832-116">U kunt ten slotte de sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3a832-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3a832-117">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="3a832-117">What you learn</span></span>

* <span data-ttu-id="3a832-118">Het maken van een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="3a832-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="3a832-119">Klik hier voor meer informatie over het Edison verbinden met een temperatuursensor Groove.</span><span class="sxs-lookup"><span data-stu-id="3a832-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="3a832-120">Klik hier voor meer informatie over het verzamelen van sensorgegevens met een voorbeeld van toepassing op Edison uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3a832-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="3a832-121">Hoe sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3a832-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3a832-122">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="3a832-122">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="3a832-124">De Intel Edison-kaart</span><span class="sxs-lookup"><span data-stu-id="3a832-124">The Intel Edison board</span></span>
* <span data-ttu-id="3a832-125">Arduino uitbreiding mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="3a832-125">Arduino expansion board</span></span>
* <span data-ttu-id="3a832-126">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a832-126">An active Azure subscription.</span></span> <span data-ttu-id="3a832-127">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="3a832-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3a832-128">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3a832-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="3a832-129">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="3a832-129">An Internet connection.</span></span>
* <span data-ttu-id="3a832-130">Een B Micro van Type A USB-kabel</span><span class="sxs-lookup"><span data-stu-id="3a832-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="3a832-131">Een voeding direct huidige (DC).</span><span class="sxs-lookup"><span data-stu-id="3a832-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="3a832-132">Het prioriteitsniveau van uw voeding moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="3a832-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="3a832-133">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="3a832-133">7-15V DC</span></span>
  - <span data-ttu-id="3a832-134">Ten minste 1500mA</span><span class="sxs-lookup"><span data-stu-id="3a832-134">At least 1500mA</span></span>
  - <span data-ttu-id="3a832-135">De pincode center/interne moet de positieve pool van de voeding</span><span class="sxs-lookup"><span data-stu-id="3a832-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="3a832-136">De volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="3a832-136">The following items are optional:</span></span>

* <span data-ttu-id="3a832-137">Groove Base schild V2</span><span class="sxs-lookup"><span data-stu-id="3a832-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="3a832-138">Groove - temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="3a832-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="3a832-139">Groove-kabel</span><span class="sxs-lookup"><span data-stu-id="3a832-139">Grove Cable</span></span>
* <span data-ttu-id="3a832-140">Een tussenruimte balken of schroeven opgenomen in de verpakking, met inbegrip van twee schroeven om de module aan de bestuur uitbreiding en vier sets schroeven en plastic spacers bevestigen.</span><span class="sxs-lookup"><span data-stu-id="3a832-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="3a832-141">Deze items zijn optioneel, omdat de ondersteuning voor het voorbeeld van code sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="3a832-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="3a832-142">Intel Edison instellen</span><span class="sxs-lookup"><span data-stu-id="3a832-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="3a832-143">Het mededelingenbord samenstellen</span><span class="sxs-lookup"><span data-stu-id="3a832-143">Assemble your board</span></span>

<span data-ttu-id="3a832-144">Deze sectie bevat stappen om uw module Intel® Edison koppelen aan het mededelingenbord uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="3a832-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="3a832-145">Plaats de Intel® Edison module binnen het wit overzicht op het mededelingenbord uitbreiding uitgelijnd in de gaten in de module met de schroeven op het mededelingenbord van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="3a832-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="3a832-146">Druk op de module onder de woorden `What will you make?` totdat u denkt een module dat.</span><span class="sxs-lookup"><span data-stu-id="3a832-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![het mededelingenbord 2 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="3a832-148">De twee hexadecimale nuts (opgenomen in het pakket) gebruiken voor het beveiligen van de module in op het mededelingenbord van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="3a832-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![het mededelingenbord 3 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="3a832-150">Voeg een installatie in een van de vier hoek gaten op het mededelingenbord van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="3a832-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="3a832-151">Draai en dat een van de witte plastic spacers op de installatie wordt versterkt.</span><span class="sxs-lookup"><span data-stu-id="3a832-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![het mededelingenbord 4 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="3a832-153">Herhaal voor de andere drie hoek spacers.</span><span class="sxs-lookup"><span data-stu-id="3a832-153">Repeat for the other three corner spacers.</span></span>

   ![het mededelingenbord 5 samenstellen](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="3a832-155">Nu is het mededelingenbord samengesteld.</span><span class="sxs-lookup"><span data-stu-id="3a832-155">Now your board is assembled.</span></span>

   ![samengesteld mededelingenbord](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="3a832-157">Verbinding maken met het Groove Base schild en de temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="3a832-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="3a832-158">Plaats het Groove Base schild doorsturen naar het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="3a832-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="3a832-159">Zorg ervoor dat alle pincodes goed zijn aangesloten op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="3a832-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Groove Base schild](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="3a832-161">Verbinding maken Groove-temperatuursensor naar het Groove Base schild via Groove kabel **A0** poort.</span><span class="sxs-lookup"><span data-stu-id="3a832-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Verbinding maken met-temperatuursensor](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison en sensor verbinding](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="3a832-164">Nu is uw sensor gereed.</span><span class="sxs-lookup"><span data-stu-id="3a832-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="3a832-165">Geef Edison</span><span class="sxs-lookup"><span data-stu-id="3a832-165">Power up Edison</span></span>

1. <span data-ttu-id="3a832-166">Sluit de voeding.</span><span class="sxs-lookup"><span data-stu-id="3a832-166">Plug in the power supply.</span></span>

   ![Plug-in-voeding](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="3a832-168">Een groene LED (met de naam DS1 op het mededelingenbord Arduino * uitbreiding) moet branden en blijf branden.</span><span class="sxs-lookup"><span data-stu-id="3a832-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="3a832-169">Wacht een minuut voor de kaart te voltooien wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="3a832-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a832-170">Als u een DC-voeding niet hebt, kunt u nog steeds het mededelingenbord via een USB-poort voor energiebeheer.</span><span class="sxs-lookup"><span data-stu-id="3a832-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="3a832-171">Zie `Connect Edison to your computer` sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3a832-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="3a832-172">Dat het mededelingenbord op deze manier kan leiden tot onvoorspelbaar gedrag van het mededelingenbord vooral wanneer met behulp van Wi-Fi of groot motoren.</span><span class="sxs-lookup"><span data-stu-id="3a832-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="3a832-173">Edison aansluiten op uw computer</span><span class="sxs-lookup"><span data-stu-id="3a832-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="3a832-174">Schakelen naar beneden de microswitch naar de twee micro USB-poorten, zodat Edison in de apparaatmodus.</span><span class="sxs-lookup"><span data-stu-id="3a832-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="3a832-175">Raadpleeg voor de verschillen tussen het apparaat en host-modus, [hier](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="3a832-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Uitschakelen van de microswitch](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="3a832-177">De micro USB-kabel aansluiten op de bovenste micro USB-poort.</span><span class="sxs-lookup"><span data-stu-id="3a832-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Bovenste micro USB-poort](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="3a832-179">Het andere einde van USB-kabel aansluiten op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3a832-179">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="3a832-181">Weet u dat het mededelingenbord volledig is geïnitialiseerd, wanneer uw computer koppelt een nieuw station (net zoals een SD-kaart in uw computer invoegen).</span><span class="sxs-lookup"><span data-stu-id="3a832-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="3a832-182">Downloaden en uitvoeren van het configuratiehulpprogramma</span><span class="sxs-lookup"><span data-stu-id="3a832-182">Download and run the configuration tool</span></span>
<span data-ttu-id="3a832-183">Ophalen van de nieuwste hulpprogramma voor serverconfiguratie van [deze koppeling](https://software.intel.com/en-us/iot/hardware/edison/downloads) vermeld in de `Installers` kop.</span><span class="sxs-lookup"><span data-stu-id="3a832-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="3a832-184">Het hulpprogramma uitvoeren en volg de aanwijzingen op het scherm instructies en klik vervolgens op waar nodig</span><span class="sxs-lookup"><span data-stu-id="3a832-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="3a832-185">Flash-firmware</span><span class="sxs-lookup"><span data-stu-id="3a832-185">Flash firmware</span></span>
1. <span data-ttu-id="3a832-186">Op de `Set up options` pagina, klikt u op `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="3a832-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="3a832-187">Selecteer de installatiekopie moet op het mededelingenbord flash op een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="3a832-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="3a832-188">Als u wilt downloaden en het mededelingenbord met de meest recente firmware-installatiekopie beschikbaar van Intel flash, selecteer `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="3a832-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="3a832-189">Selecteer Flash het mededelingenbord met een installatiekopie die u al hebt opgeslagen op uw computer, `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="3a832-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="3a832-190">Blader naar en selecteer de installatiekopie die u wilt flash op het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="3a832-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="3a832-191">Het hulpprogramma setup probeert te flash het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="3a832-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="3a832-192">Het hele knipperende proces kan maximaal 10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3a832-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="3a832-193">Wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="3a832-193">Set password</span></span>
1. <span data-ttu-id="3a832-194">Op de `Set up options` pagina, klikt u op `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="3a832-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="3a832-195">U kunt een aangepaste naam voor uw kaart Intel® Edison instellen.</span><span class="sxs-lookup"><span data-stu-id="3a832-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="3a832-196">Dit is optioneel.</span><span class="sxs-lookup"><span data-stu-id="3a832-196">This is optional.</span></span>
3. <span data-ttu-id="3a832-197">Typ een wachtwoord voor uw kaart en klik vervolgens op `Set password`.</span><span class="sxs-lookup"><span data-stu-id="3a832-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="3a832-198">Markeert u het wachtwoord dat later wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3a832-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="3a832-199">Wi-Fi-verbinding</span><span class="sxs-lookup"><span data-stu-id="3a832-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="3a832-200">Op de `Set up options` pagina, klikt u op `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="3a832-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="3a832-201">Wacht maximaal één minuut als uw computer wordt gescand naar beschikbare Wi-Fi-netwerken.</span><span class="sxs-lookup"><span data-stu-id="3a832-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="3a832-202">Van de `Detected Networks` vervolgkeuzelijst, selecteert u uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="3a832-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="3a832-203">Van de `Security` vervolgkeuzelijst Selecteer beveiligingstype van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="3a832-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="3a832-204">Geef informatie op uw aanmeldingsnaam en het wachtwoord en klik vervolgens op `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="3a832-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="3a832-205">Markeer de IP-adres, die later wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3a832-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="3a832-206">Zorg ervoor dat Edison is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="3a832-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="3a832-207">Uw computer verbinding maakt met uw Edison met behulp van het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3a832-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Verbinding maken met-temperatuursensor](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="3a832-209">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="3a832-209">Congratulations!</span></span> <span data-ttu-id="3a832-210">U hebt Edison geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3a832-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="3a832-211">Een voorbeeld van een toepassing uitvoeren op Intel Edison</span><span class="sxs-lookup"><span data-stu-id="3a832-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="3a832-212">Het apparaat met Azure IoT SDK voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3a832-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="3a832-213">Gebruik een van de volgende SSH-clients van de hostcomputer verbinding maken met uw Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="3a832-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="3a832-214">Het IP-adres is van het configuratiehulpprogramma en het wachtwoord is de taak die u hebt ingesteld in dat hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="3a832-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="3a832-215">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="3a832-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="3a832-216">De ingebouwde SSH-client op Ubuntu- of Mac OS (uitvoeren `ssh root@"the IP address"`).</span><span class="sxs-lookup"><span data-stu-id="3a832-216">The built-in SSH client on Ubuntu or macOS (run `ssh root@"the IP address"`).</span></span>

2. <span data-ttu-id="3a832-217">Kloon de voorbeeld-client-app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3a832-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="3a832-218">Navigeer naar de map opslagplaats naar de volgende opdracht voor het bouwen van Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="3a832-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-the-sample-application"></a><span data-ttu-id="3a832-219">De voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="3a832-219">Configure the sample application</span></span>

1. <span data-ttu-id="3a832-220">Open het configuratiebestand met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3a832-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Configuratiebestand](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="3a832-222">Er zijn twee macro's in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="3a832-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="3a832-223">De eerste is `INTERVAL`, definieert het tijdsinterval tussen twee berichten die naar de cloud verzendt.</span><span class="sxs-lookup"><span data-stu-id="3a832-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="3a832-224">De tweede waarde `SIMULATED_DATA`, dit is een Booleaanse waarde voor of gesimuleerde sensorgegevens of niet.</span><span class="sxs-lookup"><span data-stu-id="3a832-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="3a832-225">Als u **hoeft niet de sensor**stelt de `SIMULATED_DATA` van waarde naar `1` ervoor dat de voorbeeldtoepassing maken en gebruiken van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="3a832-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="3a832-226">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="3a832-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="3a832-227">De voorbeeldtoepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3a832-227">Build and run the sample application</span></span>

1. <span data-ttu-id="3a832-228">De voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a832-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Uitvoer bouwen](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="3a832-230">De voorbeeldtoepassing met de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3a832-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="3a832-231">Zorg ervoor dat u kopiëren en plakken de apparaat-verbindingsreeks in enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="3a832-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="3a832-232">Hier ziet u de volgende uitvoer waarin de sensorgegevens en de berichten die worden verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3a832-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - sensorgegevens verzonden van Intel Edison naar uw IoT-hub](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="3a832-234">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a832-234">Next steps</span></span>

<span data-ttu-id="3a832-235">U kunt een voorbeeldtoepassing sensorgegevens verzamelen en verzenden naar uw IoT-hub hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3a832-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
