---
title: Raspberry Pi naar cloud (Node.js) - frambozen Pi verbinding maken met Azure IoT Hub | Microsoft Docs
description: Frambozen Pi verbinding met Azure IoT Hub voor frambozen Pi gegevens verzenden naar de Azure-cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot raspberry pi, raspberry pi iothub, raspberry pi verzenden gegevens naar de cloud, raspberry pi naar cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="10a9c-104">Raspberry Pi verbinden met Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="10a9c-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="10a9c-105">In deze zelfstudie maakt beginnen u door te leren over het werken met frambozen Pi met Raspbian.</span><span class="sxs-lookup"><span data-stu-id="10a9c-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="10a9c-106">Vervolgens leert u hoe u uw apparaten probleemloos verbinding met de cloud via [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="10a9c-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="10a9c-107">Voor voorbeelden van Windows 10 IoT-Core, gaat u naar de [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="10a9c-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="10a9c-108">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="10a9c-108">Don't have a kit yet?</span></span> <span data-ttu-id="10a9c-109">Probeer de [frambozen Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="10a9c-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="10a9c-110">Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="10a9c-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="10a9c-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="10a9c-111">What you do</span></span>

* <span data-ttu-id="10a9c-112">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="10a9c-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="10a9c-113">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="10a9c-113">Create an IoT hub.</span></span>
* <span data-ttu-id="10a9c-114">Een apparaat registreren voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10a9c-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="10a9c-115">Een voorbeeld van een toepassing uitvoeren op Pi sensorgegevens verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10a9c-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="10a9c-116">Verbinding maken met frambozen Pi naar een IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="10a9c-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="10a9c-117">Vervolgens voert u een voorbeeld van toepassing op Pi temperatuur en vochtigheid om gegevens te verzamelen van een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="10a9c-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="10a9c-118">U kunt ten slotte de sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10a9c-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="10a9c-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="10a9c-119">What you learn</span></span>

* <span data-ttu-id="10a9c-120">Het maken van een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="10a9c-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="10a9c-121">Klik hier voor meer informatie over het Pi verbinden met een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="10a9c-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="10a9c-122">Klik hier voor meer informatie over het verzamelen van sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="10a9c-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="10a9c-123">Hoe sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10a9c-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="10a9c-124">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="10a9c-124">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="10a9c-126">De frambozen Pi 2 of frambozen Pi 3-kaart.</span><span class="sxs-lookup"><span data-stu-id="10a9c-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="10a9c-127">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="10a9c-127">An active Azure subscription.</span></span> <span data-ttu-id="10a9c-128">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="10a9c-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="10a9c-129">Een monitor, een USB-toetsenbord en muis die verbinding met Pi maken.</span><span class="sxs-lookup"><span data-stu-id="10a9c-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="10a9c-130">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10a9c-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="10a9c-131">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="10a9c-131">An Internet connection.</span></span>
* <span data-ttu-id="10a9c-132">Een 16 GB of hoger microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="10a9c-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="10a9c-133">Een USB-SD adapter of microSD-kaart branden van de installatiekopie van het besturingssysteem op de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="10a9c-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="10a9c-134">Een 5-v 2 amp voeding met 6 mond micro USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="10a9c-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="10a9c-135">De volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="10a9c-135">The following items are optional:</span></span>

* <span data-ttu-id="10a9c-136">Een samengesteld Adafruit BME280 temperatuur, druk en vochtigheid sensor.</span><span class="sxs-lookup"><span data-stu-id="10a9c-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="10a9c-137">Een breadboard.</span><span class="sxs-lookup"><span data-stu-id="10a9c-137">A breadboard.</span></span>
* <span data-ttu-id="10a9c-138">6 F/M meestal bedrading.</span><span class="sxs-lookup"><span data-stu-id="10a9c-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="10a9c-139">Een gedempt 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="10a9c-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="10a9c-140">Deze items zijn optioneel, omdat de ondersteuning voor het voorbeeld van code sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="10a9c-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="10a9c-141">Raspberry Pi instellen</span><span class="sxs-lookup"><span data-stu-id="10a9c-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="10a9c-142">Het besturingssysteem Raspbian voor Pi installeren</span><span class="sxs-lookup"><span data-stu-id="10a9c-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="10a9c-143">Bereid de microSD-kaart voor de installatie van de installatiekopie van het Raspbian.</span><span class="sxs-lookup"><span data-stu-id="10a9c-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="10a9c-144">Raspbian downloaden.</span><span class="sxs-lookup"><span data-stu-id="10a9c-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="10a9c-145">[Download Raspbian Jessie met Pixel](https://www.raspberrypi.org/downloads/raspbian/) (het ZIP-bestand).</span><span class="sxs-lookup"><span data-stu-id="10a9c-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="10a9c-146">Pak de installatiekopie van het Raspbian naar een map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="10a9c-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="10a9c-147">Installeer Raspbian naar de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="10a9c-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="10a9c-148">[Download en installeer het hulpprogramma Etcher SD-kaart brander](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="10a9c-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="10a9c-149">Voer Etcher en selecteer de installatiekopie van het Raspbian die u hebt opgehaald in stap 1.</span><span class="sxs-lookup"><span data-stu-id="10a9c-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="10a9c-150">Selecteer het station microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="10a9c-150">Select the microSD card drive.</span></span> <span data-ttu-id="10a9c-151">Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd de juiste station.</span><span class="sxs-lookup"><span data-stu-id="10a9c-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="10a9c-152">Klik op Flash voor het installeren van Raspbian naar de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="10a9c-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="10a9c-153">Verwijder de microSD-kaart van uw computer wanneer de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="10a9c-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="10a9c-154">Het is veilig worden verwijderd, de microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of ontkoppelt de microSD-kaart is voltooid.</span><span class="sxs-lookup"><span data-stu-id="10a9c-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="10a9c-155">Plaats de microSD-kaart in Pi.</span><span class="sxs-lookup"><span data-stu-id="10a9c-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="10a9c-156">SSH- en I2C inschakelen</span><span class="sxs-lookup"><span data-stu-id="10a9c-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="10a9c-157">Verbinding maken met Pi de monitor, toetsenbord en muis Pi start en meld u daarna Raspbian met behulp van `pi` als de gebruikersnaam en `raspberry` als het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="10a9c-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="10a9c-158">Klik op het pictogram Raspberry > **voorkeuren** > **frambozen Pi configuratie**.</span><span class="sxs-lookup"><span data-stu-id="10a9c-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Het menu Raspbian voorkeuren](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="10a9c-160">Op de **Interfaces** tabblad, stelt u **I2C** en **SSH** naar **inschakelen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="10a9c-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="10a9c-161">Als u geen fysieke sensoren hebben en gesimuleerde sensorgegevens wilt gebruiken, is deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="10a9c-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="10a9c-163">Voor het inschakelen van SSH en I2C, vindt u meer verwijzing documenten op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="10a9c-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="10a9c-164">Verbinding maken met de sensor Pi</span><span class="sxs-lookup"><span data-stu-id="10a9c-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="10a9c-165">Gebruik de bedrading breadboard en meestal als volgt een LED en een BME280 tot Pi verbinden.</span><span class="sxs-lookup"><span data-stu-id="10a9c-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="10a9c-166">Als u niet de sensor hebt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="10a9c-166">If you don’t have the sensor, skip this section.</span></span>

![De verbinding frambozen Pi en temperatuursensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="10a9c-168">De sensor BME280 kunt temperatuur en vochtigheid gegevens verzamelen.</span><span class="sxs-lookup"><span data-stu-id="10a9c-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="10a9c-169">En de LED knippert als er een communicatie tussen het apparaat en de cloud.</span><span class="sxs-lookup"><span data-stu-id="10a9c-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="10a9c-170">Gebruik de volgende bedrading voor sensor-pincodes:</span><span class="sxs-lookup"><span data-stu-id="10a9c-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="10a9c-171">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="10a9c-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="10a9c-172">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="10a9c-172">End (Board)</span></span>            | <span data-ttu-id="10a9c-173">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="10a9c-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="10a9c-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="10a9c-175">3, 3v PWR (pincode 1)</span><span class="sxs-lookup"><span data-stu-id="10a9c-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="10a9c-176">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-176">White cable</span></span>   |
| <span data-ttu-id="10a9c-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="10a9c-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="10a9c-178">GND (pincode 6)</span><span class="sxs-lookup"><span data-stu-id="10a9c-178">GND (Pin 6)</span></span>            | <span data-ttu-id="10a9c-179">Bruine-kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-179">Brown cable</span></span>   |
| <span data-ttu-id="10a9c-180">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="10a9c-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="10a9c-181">I2C1 SDA (pincode 3)</span><span class="sxs-lookup"><span data-stu-id="10a9c-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="10a9c-182">Oranje-kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-182">Orange cable</span></span>  |
| <span data-ttu-id="10a9c-183">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="10a9c-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="10a9c-184">I2C1 SCL (pincode 5)</span><span class="sxs-lookup"><span data-stu-id="10a9c-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="10a9c-185">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-185">Red cable</span></span>     |
| <span data-ttu-id="10a9c-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="10a9c-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="10a9c-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="10a9c-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="10a9c-188">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-188">White cable</span></span>   |
| <span data-ttu-id="10a9c-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="10a9c-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="10a9c-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="10a9c-190">GND (Pin 20)</span></span>           | <span data-ttu-id="10a9c-191">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="10a9c-191">Black cable</span></span>   |

<span data-ttu-id="10a9c-192">Klik hier voor weergave [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.</span><span class="sxs-lookup"><span data-stu-id="10a9c-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="10a9c-193">Nadat u hebt BME280 is verbonden met uw Pi frambozen, moet zoals hieronder installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="10a9c-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="10a9c-195">Pi verbinding met het netwerk</span><span class="sxs-lookup"><span data-stu-id="10a9c-195">Connect Pi to the network</span></span>

<span data-ttu-id="10a9c-196">Pi inschakelen met behulp van het micro USB-kabel en de voeding.</span><span class="sxs-lookup"><span data-stu-id="10a9c-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="10a9c-197">Via het Ethernet-kabel Pi verbinden met het bekabelde netwerk of volgen de [instructies van de frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi verbinding met uw draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="10a9c-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="10a9c-198">Nadat uw Pi is verbonden met het netwerk, moet u Noteer de [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="10a9c-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Verbonden met een bekabeld netwerk](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="10a9c-200">Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="10a9c-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="10a9c-201">Bijvoorbeeld, als uw computer is verbonden met een draadloos netwerk als Pi is verbonden met een bekabeld netwerk, ziet u mogelijk niet het IP-adres in de uitvoer devdisco.</span><span class="sxs-lookup"><span data-stu-id="10a9c-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="10a9c-202">Een voorbeeld van een toepassing uitvoeren op Pi</span><span class="sxs-lookup"><span data-stu-id="10a9c-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="10a9c-203">Klonen van de voorbeeldtoepassing en de vereiste pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="10a9c-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="10a9c-204">Gebruik een van de volgende SSH-clients van de hostcomputer verbinding maken met uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="10a9c-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="10a9c-205">[PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="10a9c-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="10a9c-206">U moet het IP-adres van uw Pi zodat deze verbinding te maken via SSH.</span><span class="sxs-lookup"><span data-stu-id="10a9c-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="10a9c-207">De ingebouwde SSH-client op Ubuntu- of Mac OS.</span><span class="sxs-lookup"><span data-stu-id="10a9c-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="10a9c-208">U moet uitvoeren `ssh pi@<ip address of pi>` Pi via SSH verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="10a9c-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="10a9c-209">De standaardgebruikersnaam `pi` , en het wachtwoord is `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="10a9c-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="10a9c-210">Node.js en NPM naar uw Pi installeren.</span><span class="sxs-lookup"><span data-stu-id="10a9c-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="10a9c-211">Controleer eerst uw Node.js-versie met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="10a9c-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="10a9c-212">Als de versie lager dan 4.x is of er geen Node.js op uw Pi is, voer de volgende opdracht installeren of bijwerken van Node.js.</span><span class="sxs-lookup"><span data-stu-id="10a9c-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="10a9c-213">Kloon de voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="10a9c-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="10a9c-214">Installeer alle pakketten met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="10a9c-214">Install all packages by the following command.</span></span> <span data-ttu-id="10a9c-215">Omvat Azure IoT-device SDK, BME280 Sensor-bibliotheek en bedrading Pi-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="10a9c-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="10a9c-216">Het duurt enkele minuten duren deze denpening installatie proces op de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="10a9c-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="10a9c-217">De voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="10a9c-217">Configure the sample application</span></span>

1. <span data-ttu-id="10a9c-218">Open het configuratiebestand met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="10a9c-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Configuratiebestand](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="10a9c-220">Er zijn twee items in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="10a9c-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="10a9c-221">De eerste is `interval`, definieert het tijdsinterval tussen twee berichten die naar de cloud verzendt.</span><span class="sxs-lookup"><span data-stu-id="10a9c-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="10a9c-222">De tweede waarde `simulatedData`, dit is een Booleaanse waarde voor of gesimuleerde sensorgegevens of niet.</span><span class="sxs-lookup"><span data-stu-id="10a9c-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="10a9c-223">Als u **hoeft niet de sensor**stelt de `simulatedData` van waarde naar `true` ervoor dat de voorbeeldtoepassing maken en gebruiken van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="10a9c-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="10a9c-224">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="10a9c-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="10a9c-225">De voorbeeldtoepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="10a9c-225">Run the sample application</span></span>

1. <span data-ttu-id="10a9c-226">De voorbeeldtoepassing met de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="10a9c-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="10a9c-227">Zorg ervoor dat u kopiëren en plakken de apparaat-verbindingsreeks in enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="10a9c-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="10a9c-228">Hier ziet u de volgende uitvoer waarin de sensorgegevens en de berichten die worden verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10a9c-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - sensorgegevens verzonden van frambozen Pi naar uw IoT-hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="10a9c-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10a9c-230">Next steps</span></span>

<span data-ttu-id="10a9c-231">U kunt een voorbeeldtoepassing sensorgegevens verzamelen en verzenden naar uw IoT-hub hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="10a9c-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]