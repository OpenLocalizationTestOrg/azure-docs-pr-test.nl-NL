---
title: Raspberry Pi naar cloud (Python) - frambozen Pi verbinding maken met Azure IoT Hub | Microsoft Docs
description: Informatie over het instellen en frambozen Pi verbinden met Azure IoT Hub voor frambozen Pi gegevens verzenden naar het Azure-cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot raspberry pi, raspberry pi iothub, raspberry pi verzenden gegevens naar de cloud, raspberry pi naar cloud
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="bd276-104">Raspberry Pi verbinden met Azure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="bd276-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="bd276-105">In deze zelfstudie maakt beginnen u door te leren over het werken met frambozen Pi met Raspbian.</span><span class="sxs-lookup"><span data-stu-id="bd276-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="bd276-106">Vervolgens leert u hoe u uw apparaten probleemloos verbinding met de cloud via [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="bd276-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="bd276-107">Voor voorbeelden van Windows 10 IoT-Core, gaat u naar de [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="bd276-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="bd276-108">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="bd276-108">Don't have a kit yet?</span></span> <span data-ttu-id="bd276-109">Probeer [frambozen Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bd276-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="bd276-110">Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="bd276-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="bd276-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="bd276-111">What you do</span></span>

* <span data-ttu-id="bd276-112">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="bd276-112">Create an IoT hub.</span></span>
* <span data-ttu-id="bd276-113">Een apparaat registreren voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bd276-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="bd276-114">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="bd276-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="bd276-115">Een voorbeeld van een toepassing uitvoeren op Pi sensorgegevens verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bd276-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="bd276-116">Verbinding maken met frambozen Pi naar een IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="bd276-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="bd276-117">Vervolgens voert u een voorbeeld van toepassing op Pi temperatuur en vochtigheid om gegevens te verzamelen van een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="bd276-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="bd276-118">U kunt ten slotte de sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bd276-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="bd276-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="bd276-119">What you learn</span></span>

* <span data-ttu-id="bd276-120">Het maken van een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="bd276-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="bd276-121">Klik hier voor meer informatie over het Pi verbinden met een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="bd276-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="bd276-122">Klik hier voor meer informatie over het verzamelen van sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="bd276-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="bd276-123">Hoe sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bd276-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bd276-124">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="bd276-124">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="bd276-126">De frambozen Pi 2 of frambozen Pi 3-kaart.</span><span class="sxs-lookup"><span data-stu-id="bd276-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="bd276-127">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bd276-127">An active Azure subscription.</span></span> <span data-ttu-id="bd276-128">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="bd276-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="bd276-129">Een monitor, een USB-toetsenbord en muis die verbinding met Pi maken.</span><span class="sxs-lookup"><span data-stu-id="bd276-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="bd276-130">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd276-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="bd276-131">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="bd276-131">An Internet connection.</span></span>
* <span data-ttu-id="bd276-132">Een 16 GB of hoger microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="bd276-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="bd276-133">Een USB-SD adapter of microSD-kaart branden van de installatiekopie van het besturingssysteem op de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="bd276-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="bd276-134">Een 5-v 2 amp voeding met 6 mond micro USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="bd276-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="bd276-135">De volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="bd276-135">The following items are optional:</span></span>

* <span data-ttu-id="bd276-136">Een samengesteld Adafruit BME280 temperatuur, druk en vochtigheid sensor.</span><span class="sxs-lookup"><span data-stu-id="bd276-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="bd276-137">Een breadboard.</span><span class="sxs-lookup"><span data-stu-id="bd276-137">A breadboard.</span></span>
* <span data-ttu-id="bd276-138">6 F/M meestal bedrading.</span><span class="sxs-lookup"><span data-stu-id="bd276-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="bd276-139">Een gedempt 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="bd276-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="bd276-140">Deze items zijn optioneel, omdat de ondersteuning voor het voorbeeld van code sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="bd276-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="bd276-141">Frambozen Pi instellen</span><span class="sxs-lookup"><span data-stu-id="bd276-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="bd276-142">Het besturingssysteem Raspbian voor Pi installeren</span><span class="sxs-lookup"><span data-stu-id="bd276-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="bd276-143">Bereid de microSD-kaart voor de installatie van de installatiekopie van het Raspbian.</span><span class="sxs-lookup"><span data-stu-id="bd276-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="bd276-144">Raspbian downloaden.</span><span class="sxs-lookup"><span data-stu-id="bd276-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="bd276-145">[Raspbian Jessie met bureaublad downloaden](https://www.raspberrypi.org/downloads/raspbian/) (het ZIP-bestand).</span><span class="sxs-lookup"><span data-stu-id="bd276-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="bd276-146">Pak de installatiekopie van het Raspbian naar een map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="bd276-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="bd276-147">Installeer Raspbian naar de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="bd276-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="bd276-148">[Download en installeer het hulpprogramma Etcher SD-kaart brander](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="bd276-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="bd276-149">Voer Etcher en selecteer de installatiekopie van het Raspbian die u hebt opgehaald in stap 1.</span><span class="sxs-lookup"><span data-stu-id="bd276-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="bd276-150">Selecteer het station microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="bd276-150">Select the microSD card drive.</span></span> <span data-ttu-id="bd276-151">Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd de juiste station.</span><span class="sxs-lookup"><span data-stu-id="bd276-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="bd276-152">Klik op Flash voor het installeren van Raspbian naar de microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="bd276-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="bd276-153">Verwijder de microSD-kaart van uw computer wanneer de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="bd276-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="bd276-154">Het is veilig worden verwijderd, de microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of ontkoppelt de microSD-kaart is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bd276-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="bd276-155">Plaats de microSD-kaart in Pi.</span><span class="sxs-lookup"><span data-stu-id="bd276-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="bd276-156">SSH- en I2C inschakelen</span><span class="sxs-lookup"><span data-stu-id="bd276-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="bd276-157">Verbinding maken met Pi de monitor, toetsenbord en muis Pi start en meld u daarna Raspbian met behulp van `pi` als de gebruikersnaam en `raspberry` als het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="bd276-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="bd276-158">Klik op het pictogram Raspberry > **voorkeuren** > **frambozen Pi configuratie**.</span><span class="sxs-lookup"><span data-stu-id="bd276-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Het menu Raspbian voorkeuren](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="bd276-160">Op de **Interfaces** tabblad, stelt u **I2C** en **SSH** naar **inschakelen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd276-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="bd276-161">Als u geen fysieke sensoren hebben en gesimuleerde sensorgegevens wilt gebruiken, is deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="bd276-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="bd276-163">Voor het inschakelen van SSH en I2C, vindt u meer verwijzing documenten op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="bd276-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="bd276-164">Verbinding maken met de sensor Pi</span><span class="sxs-lookup"><span data-stu-id="bd276-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="bd276-165">Gebruik de bedrading breadboard en meestal als volgt een LED en een BME280 tot Pi verbinden.</span><span class="sxs-lookup"><span data-stu-id="bd276-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="bd276-166">Als u de sensor geen [deze sectie overslaan](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="bd276-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![De verbinding frambozen Pi en temperatuursensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="bd276-168">De sensor BME280 kunt temperatuur en vochtigheid gegevens verzamelen.</span><span class="sxs-lookup"><span data-stu-id="bd276-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="bd276-169">En de LED knippert als er een communicatie tussen het apparaat en de cloud.</span><span class="sxs-lookup"><span data-stu-id="bd276-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="bd276-170">Gebruik de volgende bedrading voor sensor-pincodes:</span><span class="sxs-lookup"><span data-stu-id="bd276-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="bd276-171">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="bd276-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="bd276-172">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="bd276-172">End (Board)</span></span>            | <span data-ttu-id="bd276-173">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="bd276-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="bd276-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="bd276-175">3, 3v PWR (pincode 1)</span><span class="sxs-lookup"><span data-stu-id="bd276-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="bd276-176">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-176">White cable</span></span>   |
| <span data-ttu-id="bd276-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="bd276-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="bd276-178">GND (pincode 6)</span><span class="sxs-lookup"><span data-stu-id="bd276-178">GND (Pin 6)</span></span>            | <span data-ttu-id="bd276-179">Bruine-kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-179">Brown cable</span></span>   |
| <span data-ttu-id="bd276-180">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="bd276-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="bd276-181">I2C1 SDA (pincode 3)</span><span class="sxs-lookup"><span data-stu-id="bd276-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="bd276-182">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-182">Red cable</span></span>     |
| <span data-ttu-id="bd276-183">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="bd276-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="bd276-184">I2C1 SCL (pincode 5)</span><span class="sxs-lookup"><span data-stu-id="bd276-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="bd276-185">Oranje-kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-185">Orange cable</span></span>  |
| <span data-ttu-id="bd276-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="bd276-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="bd276-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="bd276-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="bd276-188">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-188">White cable</span></span>   |
| <span data-ttu-id="bd276-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="bd276-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="bd276-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="bd276-190">GND (Pin 20)</span></span>           | <span data-ttu-id="bd276-191">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="bd276-191">Black cable</span></span>   |

<span data-ttu-id="bd276-192">Klik hier voor weergave [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.</span><span class="sxs-lookup"><span data-stu-id="bd276-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="bd276-193">Nadat u hebt BME280 is verbonden met uw Pi frambozen, moet zoals hieronder installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="bd276-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="bd276-195">Pi verbinding met het netwerk</span><span class="sxs-lookup"><span data-stu-id="bd276-195">Connect Pi to the network</span></span>

<span data-ttu-id="bd276-196">Pi inschakelen met behulp van het micro USB-kabel en de voeding.</span><span class="sxs-lookup"><span data-stu-id="bd276-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="bd276-197">Via het Ethernet-kabel Pi verbinden met het bekabelde netwerk of volgen de [instructies van de frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi verbinding met uw draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="bd276-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="bd276-198">Nadat uw Pi is verbonden met het netwerk, moet u Noteer de [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="bd276-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Verbonden met een bekabeld netwerk](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="bd276-200">Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer.</span><span class="sxs-lookup"><span data-stu-id="bd276-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="bd276-201">Bijvoorbeeld, als uw computer is verbonden met een draadloos netwerk als Pi is verbonden met een bekabeld netwerk, ziet u mogelijk niet het IP-adres in de uitvoer devdisco.</span><span class="sxs-lookup"><span data-stu-id="bd276-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="bd276-202">Een voorbeeld van een toepassing uitvoeren op Pi</span><span class="sxs-lookup"><span data-stu-id="bd276-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="bd276-203">De vereiste pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="bd276-203">Install the prerequisite packages</span></span>

<span data-ttu-id="bd276-204">Gebruik een van de volgende SSH-clients van de hostcomputer verbinding maken met uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="bd276-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="bd276-205">**Windows-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="bd276-205">**Windows Users**</span></span>
   1. <span data-ttu-id="bd276-206">Download en installeer [PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="bd276-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="bd276-207">Kopieer het IP-adres van uw sectie Pi in de Host-naam (of IP-adres) en selecteer SSH als het verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="bd276-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="bd276-208">**Mac- en Ubuntu-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="bd276-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="bd276-209">Gebruik de ingebouwde SSH-client op Ubuntu- of Mac OS.</span><span class="sxs-lookup"><span data-stu-id="bd276-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="bd276-210">U wilt uitvoeren `ssh pi@<ip address of pi>` Pi via SSH verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="bd276-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="bd276-211">De standaardgebruikersnaam `pi` , en het wachtwoord is `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="bd276-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="bd276-212">De voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="bd276-212">Configure the sample application</span></span>

1. <span data-ttu-id="bd276-213">Kloon de voorbeeldtoepassing met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bd276-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="bd276-214">Open het configuratiebestand met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="bd276-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="bd276-215">Er zijn 5 macro's in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="bd276-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="bd276-216">De eerste is `MESSAGE_TIMESPAN`, definieert het tijdsinterval (in milliseconden) tussen twee berichten die naar de cloud verzendt.</span><span class="sxs-lookup"><span data-stu-id="bd276-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="bd276-217">De tweede waarde `SIMULATED_DATA`, dit is een Booleaanse waarde voor of gesimuleerde sensorgegevens of niet.</span><span class="sxs-lookup"><span data-stu-id="bd276-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="bd276-218">`I2C_ADDRESS`is het adres I2C die uw sensor BME280 is verbonden.</span><span class="sxs-lookup"><span data-stu-id="bd276-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="bd276-219">`GPIO_PIN_ADDRESS`is het adres GPIO voor uw LED.</span><span class="sxs-lookup"><span data-stu-id="bd276-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="bd276-220">Het laatste item `BLINK_TIMESPAN`, die de timespan gedefinieerd wanneer uw LED is ingeschakeld in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="bd276-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="bd276-221">Als u **hoeft niet de sensor**stelt de `SIMULATED_DATA` van waarde naar `True` ervoor dat de voorbeeldtoepassing maken en gebruiken van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="bd276-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="bd276-222">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="bd276-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="bd276-223">De voorbeeldtoepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bd276-223">Build and run the sample application</span></span>

1. <span data-ttu-id="bd276-224">De voorbeeldtoepassing door de volgende opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="bd276-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="bd276-225">Omdat de Azure IoT SDK's voor Python wrappers boven op de C-SDK van Azure IoT-apparaat, moet u de C-bibliotheken worden gecompileerd als voor het genereren van de Python-bibliotheken van broncode moet of wilt u.</span><span class="sxs-lookup"><span data-stu-id="bd276-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="bd276-226">U kunt ook opgeven met de versie die u wilt dat door het uitvoeren van `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="bd276-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="bd276-227">Als u het script zonder parameter uitvoert, het script detecteert automatisch de versie van python geïnstalleerd (zoekvolgorde 2.7 -> 3.4 3.5 ->).</span><span class="sxs-lookup"><span data-stu-id="bd276-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="bd276-228">Zorg ervoor dat uw versie van Python consistent blijft tijdens het bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bd276-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="bd276-229">Over het bouwen van de clientbibliotheek Python (iothub_client.so) op Linux-apparaten die minder dan 1 GB RAM-geheugen, ziet u mogelijk bouwen zitten 98% tijdens het bouwen van iothub_client_python.cpp zoals hieronder wordt weergegeven `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="bd276-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="bd276-230">Als u dit probleem ondervindt, controleert u het geheugengebruik van het apparaat via `free -m command` in een andere terminalvenster gedurende die tijd.</span><span class="sxs-lookup"><span data-stu-id="bd276-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="bd276-231">Als u onvoldoende geheugen tijdens het compileren van iothub_client_python.cpp bestand uitvoert, moet u wellicht tijdelijk vergroten de wisselruimte voor geheugen meer beschikbaar om het apparaat in Python clientzijde SDK-bibliotheek met succes samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="bd276-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="bd276-232">De voorbeeldtoepassing met de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bd276-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="bd276-233">Zorg ervoor dat u kopiëren en plakken de apparaat-verbindingsreeks in enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="bd276-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="bd276-234">En als u de python 3 gebruiken, dan kunt u de opdracht `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="bd276-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="bd276-235">Hier ziet u de volgende uitvoer waarin de sensorgegevens en de berichten die worden verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bd276-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Output - sensorgegevens verzonden van frambozen Pi naar uw IoT-hub](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="bd276-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd276-237">Next steps</span></span>

<span data-ttu-id="bd276-238">U kunt een voorbeeldtoepassing sensorgegevens verzamelen en verzenden naar uw IoT-hub hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd276-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="bd276-239">Zie voor de berichten die uw Pi frambozen is verzonden naar uw IoT-hub of verzenden berichten naar uw Pi frambozen in een opdrachtregelinterface de [beheren cloud apparaat messaging met iothub explorer zelfstudie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="bd276-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
