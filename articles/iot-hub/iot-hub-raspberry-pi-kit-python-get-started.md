---
title: aaaRaspberry Pi toocloud (Python) - verbinding frambozen Pi tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met frambozen Pi tooAzure IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot raspberry pi raspberry pi iot hub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="42c52-104">Verbinding maken met frambozen Pi tooAzure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="42c52-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="42c52-105">In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met frambozen Pi met Raspbian leren.</span><span class="sxs-lookup"><span data-stu-id="42c52-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="42c52-106">U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="42c52-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="42c52-107">Ga voor voorbeelden van Windows 10 IoT-Core, toohello [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="42c52-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="42c52-108">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="42c52-108">Don't have a kit yet?</span></span> <span data-ttu-id="42c52-109">Probeer [frambozen Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="42c52-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="42c52-110">Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="42c52-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="42c52-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="42c52-111">What you do</span></span>

* <span data-ttu-id="42c52-112">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="42c52-112">Create an IoT hub.</span></span>
* <span data-ttu-id="42c52-113">Een apparaat registreren voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42c52-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="42c52-114">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="42c52-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="42c52-115">Een voorbeeld van toepassing op tooyour iothub-Pi toosend sensor gegevens uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="42c52-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="42c52-116">Verbinding maken frambozen Pi tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="42c52-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="42c52-117">Vervolgens voert u een voorbeeld van toepassing op Pi toocollect temperatuur en vochtigheid gegevens van een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="42c52-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="42c52-118">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="42c52-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="42c52-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="42c52-119">What you learn</span></span>

* <span data-ttu-id="42c52-120">Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="42c52-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="42c52-121">Hoe tooconnect Pi met een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="42c52-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="42c52-122">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="42c52-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="42c52-123">Hoe toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42c52-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="42c52-124">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="42c52-124">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="42c52-126">Hallo frambozen Pi 2 of frambozen Pi 3 mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="42c52-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="42c52-127">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="42c52-127">An active Azure subscription.</span></span> <span data-ttu-id="42c52-128">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="42c52-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="42c52-129">Een monitor, een USB-toetsenbord en muis die tooPi verbinding.</span><span class="sxs-lookup"><span data-stu-id="42c52-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="42c52-130">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="42c52-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="42c52-131">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="42c52-131">An Internet connection.</span></span>
* <span data-ttu-id="42c52-132">Een 16 GB of hoger microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="42c52-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="42c52-133">Een USB-SD adapter of microSD-kaart tooburn Hallo besturingssysteeminstallatiekopie op Hallo microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="42c52-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="42c52-134">Een 5-v 2 amp voeding met Hallo 6 mond micro USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="42c52-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="42c52-135">Hallo volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="42c52-135">hello following items are optional:</span></span>

* <span data-ttu-id="42c52-136">Een samengesteld Adafruit BME280 temperatuur, druk en vochtigheid sensor.</span><span class="sxs-lookup"><span data-stu-id="42c52-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="42c52-137">Een breadboard.</span><span class="sxs-lookup"><span data-stu-id="42c52-137">A breadboard.</span></span>
* <span data-ttu-id="42c52-138">6 F/M meestal bedrading.</span><span class="sxs-lookup"><span data-stu-id="42c52-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="42c52-139">Een gedempt 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="42c52-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="42c52-140">Deze items zijn optioneel, omdat Hallo code voorbeeld ondersteuning sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="42c52-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="42c52-141">Frambozen Pi instellen</span><span class="sxs-lookup"><span data-stu-id="42c52-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="42c52-142">Hallo Raspbian besturingssysteem voor Pi installeren</span><span class="sxs-lookup"><span data-stu-id="42c52-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="42c52-143">Hallo microSD-kaart voor de installatie van Hallo Raspbian afbeelding voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="42c52-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="42c52-144">Raspbian downloaden.</span><span class="sxs-lookup"><span data-stu-id="42c52-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="42c52-145">[Raspbian Jessie met bureaublad downloaden](https://www.raspberrypi.org/downloads/raspbian/) (Hallo ZIP-bestand).</span><span class="sxs-lookup"><span data-stu-id="42c52-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="42c52-146">Pak Hallo Raspbian installatiekopie tooa map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="42c52-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="42c52-147">Installeer Raspbian toohello microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="42c52-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="42c52-148">[Download en installeer Hallo Etcher SD-kaart brander hulpprogramma](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="42c52-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="42c52-149">Voer Etcher en Hallo Raspbian installatiekopie die u hebt opgehaald in stap 1.</span><span class="sxs-lookup"><span data-stu-id="42c52-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="42c52-150">Selecteer Hallo microSD-kaart station.</span><span class="sxs-lookup"><span data-stu-id="42c52-150">Select hello microSD card drive.</span></span> <span data-ttu-id="42c52-151">Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd Hallo juiste station.</span><span class="sxs-lookup"><span data-stu-id="42c52-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="42c52-152">Klik op Flash tooinstall Raspbian toohello microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="42c52-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="42c52-153">Hallo microSD-kaart van uw computer verwijderen wanneer de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="42c52-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="42c52-154">Het is veilig tooremove hello microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of Hallo microSD-kaart is voltooid ontkoppelt.</span><span class="sxs-lookup"><span data-stu-id="42c52-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="42c52-155">Hallo microSD-kaart invoegen in Pi.</span><span class="sxs-lookup"><span data-stu-id="42c52-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="42c52-156">SSH- en I2C inschakelen</span><span class="sxs-lookup"><span data-stu-id="42c52-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="42c52-157">Sluit Pi toohello monitor, toetsenbord en muis, Pi starten en meld u daarna Raspbian met behulp van `pi` als Hallo-gebruikersnaam en `raspberry` Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="42c52-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="42c52-158">Klik op Hallo Raspberry pictogram > **voorkeuren** > **frambozen Pi configuratie**.</span><span class="sxs-lookup"><span data-stu-id="42c52-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Hallo Raspbian voorkeuren menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="42c52-160">Op Hallo **Interfaces** tabblad, stelt u **I2C** en **SSH** te**inschakelen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="42c52-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="42c52-161">Als u geen fysieke sensoren hebben en sensorgegevens toouse gesimuleerde wilt, moet deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="42c52-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="42c52-163">tooenable SSH en I2C u meer verwijzing documenten vindt op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="42c52-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="42c52-164">Hallo sensor tooPi verbinding</span><span class="sxs-lookup"><span data-stu-id="42c52-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="42c52-165">Hallo breadboard en meestal kabels tooconnect een LED en een tooPi BME280 als volgt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42c52-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="42c52-166">Als u geen Hallo sensor, [deze sectie overslaan](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="42c52-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hallo frambozen Pi en sensor verbinding](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="42c52-168">Hallo BME280 sensor kunt temperatuur en vochtigheid gegevens verzamelen.</span><span class="sxs-lookup"><span data-stu-id="42c52-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="42c52-169">En Hallo LED knippert als er een communicatie tussen apparaten en Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="42c52-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="42c52-170">Gebruik voor pincodes sensor, Hallo bedrading te volgen:</span><span class="sxs-lookup"><span data-stu-id="42c52-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="42c52-171">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="42c52-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="42c52-172">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="42c52-172">End (Board)</span></span>            | <span data-ttu-id="42c52-173">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="42c52-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="42c52-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="42c52-175">3, 3v PWR (pincode 1)</span><span class="sxs-lookup"><span data-stu-id="42c52-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="42c52-176">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-176">White cable</span></span>   |
| <span data-ttu-id="42c52-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="42c52-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="42c52-178">GND (pincode 6)</span><span class="sxs-lookup"><span data-stu-id="42c52-178">GND (Pin 6)</span></span>            | <span data-ttu-id="42c52-179">Bruine-kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-179">Brown cable</span></span>   |
| <span data-ttu-id="42c52-180">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="42c52-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="42c52-181">I2C1 SDA (pincode 3)</span><span class="sxs-lookup"><span data-stu-id="42c52-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="42c52-182">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-182">Red cable</span></span>     |
| <span data-ttu-id="42c52-183">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="42c52-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="42c52-184">I2C1 SCL (pincode 5)</span><span class="sxs-lookup"><span data-stu-id="42c52-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="42c52-185">Oranje-kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-185">Orange cable</span></span>  |
| <span data-ttu-id="42c52-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="42c52-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="42c52-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="42c52-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="42c52-188">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-188">White cable</span></span>   |
| <span data-ttu-id="42c52-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="42c52-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="42c52-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="42c52-190">GND (Pin 20)</span></span>           | <span data-ttu-id="42c52-191">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="42c52-191">Black cable</span></span>   |

<span data-ttu-id="42c52-192">Klik op tooview [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.</span><span class="sxs-lookup"><span data-stu-id="42c52-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="42c52-193">Nadat u verbinding hebt gemaakt BME280 tooyour frambozen Pi, moet zoals hieronder installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="42c52-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="42c52-195">Pi toohello netwerk verbinden</span><span class="sxs-lookup"><span data-stu-id="42c52-195">Connect Pi toohello network</span></span>

<span data-ttu-id="42c52-196">Pi inschakelen met behulp van Hallo micro USB-kabel en Hallo voeding.</span><span class="sxs-lookup"><span data-stu-id="42c52-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="42c52-197">Gebruik Hallo Ethernet-kabel tooconnect Pi tooyour bekabelde netwerk of volgen Hallo [instructies uit Hallo frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour draadloos netwerk.</span><span class="sxs-lookup"><span data-stu-id="42c52-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="42c52-198">Nadat uw Pi met succes verbonden toohello netwerk is, moet u een notitie van Hallo tootake [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="42c52-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired verbonden netwerk](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="42c52-200">Zorg ervoor dat Pi verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="42c52-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="42c52-201">Bijvoorbeeld, als uw computer verbonden tooa draadloze netwerk is wanneer Pi verbonden tooa standaardnetwerk is, ziet u mogelijk niet Hallo IP-adres in Hallo devdisco uitvoer.</span><span class="sxs-lookup"><span data-stu-id="42c52-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="42c52-202">Een voorbeeld van een toepassing uitvoeren op Pi</span><span class="sxs-lookup"><span data-stu-id="42c52-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="42c52-203">Vereiste hello-pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="42c52-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="42c52-204">Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour frambozen Pi Hallo.</span><span class="sxs-lookup"><span data-stu-id="42c52-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="42c52-205">**Windows-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="42c52-205">**Windows Users**</span></span>
   1. <span data-ttu-id="42c52-206">Download en installeer [PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="42c52-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="42c52-207">Kopieer Hallo IP-adres van de sectie Pi in Hallo Host name (of IP-adres) en selecteer SSH als Hallo verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="42c52-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="42c52-208">**Mac- en Ubuntu-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="42c52-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="42c52-209">Hallo ingebouwde SSH-client op Ubuntu- of Mac OS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42c52-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="42c52-210">Mogelijk moet u toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="42c52-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="42c52-211">Hallo standaardgebruikersnaam `pi` , en het Hallo-wachtwoord is `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="42c52-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="42c52-212">Hallo-voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="42c52-212">Configure hello sample application</span></span>

1. <span data-ttu-id="42c52-213">Hallo-voorbeeldtoepassing door het uitvoeren van de volgende opdracht Hallo klonen:</span><span class="sxs-lookup"><span data-stu-id="42c52-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="42c52-214">Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="42c52-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="42c52-215">Er zijn 5 macro's in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="42c52-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="42c52-216">Hallo eerst een is `MESSAGE_TIMESPAN`, definieert een Hallo tijdsinterval (in milliseconden) tussen twee berichten die toocloud verzenden.</span><span class="sxs-lookup"><span data-stu-id="42c52-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="42c52-217">tweede Hallo `SIMULATED_DATA`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="42c52-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="42c52-218">`I2C_ADDRESS`Hallo I2C-adres dat is verbonden met uw BME280 sensor is.</span><span class="sxs-lookup"><span data-stu-id="42c52-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="42c52-219">`GPIO_PIN_ADDRESS`Hallo GPIO adres is voor uw LED.</span><span class="sxs-lookup"><span data-stu-id="42c52-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="42c52-220">Hallo laatste een is `BLINK_TIMESPAN`, die Hallo timespan gedefinieerd wanneer uw LED is ingeschakeld in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="42c52-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="42c52-221">Als u **geen Hallo sensor**stelt hello `SIMULATED_DATA` waarde te`True` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42c52-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="42c52-222">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="42c52-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="42c52-223">Hallo voorbeeldtoepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="42c52-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="42c52-224">Hallo-voorbeeldtoepassing bouwen door het uitvoeren van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="42c52-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="42c52-225">Omdat hello Azure IoT SDK's voor Python wrappers boven op Hallo C-SDK van Azure IoT-apparaat, moet u toocompile Hallo C bibliotheken als toogenerate Hallo Python-bibliotheken van broncode moet of wilt u.</span><span class="sxs-lookup"><span data-stu-id="42c52-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="42c52-226">U kunt ook opgeven Hallo-versie die u wilt dat door het uitvoeren van `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="42c52-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="42c52-227">Als u het script zonder parameter uitvoert, Hallo script Hallo-versie van python geïnstalleerd automatisch detecteren (zoekvolgorde 2.7 -> 3.4 3.5 ->).</span><span class="sxs-lookup"><span data-stu-id="42c52-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="42c52-228">Zorg ervoor dat uw versie van Python consistent blijft tijdens het bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="42c52-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="42c52-229">Over het bouwen van Hallo Python-clientbibliotheek (iothub_client.so) op Linux-apparaten die minder dan 1 GB RAM-geheugen, ziet u mogelijk bouwen zitten 98% tijdens het bouwen van iothub_client_python.cpp zoals hieronder wordt weergegeven `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="42c52-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="42c52-230">Als u dit probleem ondervindt, Controleer Hallo geheugenverbruik van het Hallo-apparaten met `free -m command` in een andere terminalvenster gedurende die tijd.</span><span class="sxs-lookup"><span data-stu-id="42c52-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="42c52-231">Als u onvoldoende geheugen tijdens het compileren van iothub_client_python.cpp bestand uitvoert, hebt u mogelijk verhogen Hallo wisselen ruimte tooget tootemporarily meer beschikbaar geheugen toosuccessfully bouwen Hallo Python clientzijde apparaat SDK-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="42c52-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="42c52-232">Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="42c52-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="42c52-233">Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="42c52-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="42c52-234">En als u python Hallo 3 gebruiken, dan kunt u de opdracht Hallo `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="42c52-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="42c52-235">U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="42c52-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![Output - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="42c52-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="42c52-237">Next steps</span></span>

<span data-ttu-id="42c52-238">U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="42c52-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="42c52-239">toosee Hallo-berichten dat uw Pi frambozen tooyour IoT-hub of verzenden berichten tooyour frambozen Pi heeft verzonden in een opdrachtregelinterface Zie Hallo [beheren cloud apparaat messaging met iothub explorer zelfstudie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="42c52-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
