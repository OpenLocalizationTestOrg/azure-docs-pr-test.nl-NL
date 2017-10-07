---
title: aaaRaspberry Pi toocloud (Node.js) - verbinding frambozen Pi tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met frambozen Pi tooAzure IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot raspberry pi raspberry pi iot hub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="923f4-104">Verbinding maken met frambozen Pi tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="923f4-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="923f4-105">In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met frambozen Pi met Raspbian leren.</span><span class="sxs-lookup"><span data-stu-id="923f4-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="923f4-106">U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="923f4-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="923f4-107">Ga voor voorbeelden van Windows 10 IoT-Core, toohello [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="923f4-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="923f4-108">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="923f4-108">Don't have a kit yet?</span></span> <span data-ttu-id="923f4-109">Probeer [frambozen Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="923f4-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="923f4-110">Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="923f4-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="923f4-111">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="923f4-111">What you do</span></span>

* <span data-ttu-id="923f4-112">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="923f4-112">Create an IoT hub.</span></span>
* <span data-ttu-id="923f4-113">Een apparaat registreren voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="923f4-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="923f4-114">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="923f4-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="923f4-115">Een voorbeeld van toepassing op tooyour iothub-Pi toosend sensor gegevens uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="923f4-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="923f4-116">Verbinding maken frambozen Pi tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="923f4-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="923f4-117">Vervolgens voert u een voorbeeld van toepassing op Pi toocollect temperatuur en vochtigheid gegevens van een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="923f4-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="923f4-118">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="923f4-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="923f4-119">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="923f4-119">What you learn</span></span>

* <span data-ttu-id="923f4-120">Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="923f4-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="923f4-121">Hoe tooconnect Pi met een sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="923f4-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="923f4-122">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.</span><span class="sxs-lookup"><span data-stu-id="923f4-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="923f4-123">Hoe toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="923f4-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="923f4-124">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="923f4-124">What you need</span></span>

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="923f4-126">Hallo frambozen Pi 2 of frambozen Pi 3 mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="923f4-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="923f4-127">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="923f4-127">An active Azure subscription.</span></span> <span data-ttu-id="923f4-128">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="923f4-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="923f4-129">Een monitor, een USB-toetsenbord en muis die tooPi verbinding.</span><span class="sxs-lookup"><span data-stu-id="923f4-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="923f4-130">Een Mac of een PC die Windows of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="923f4-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="923f4-131">Een internetverbinding.</span><span class="sxs-lookup"><span data-stu-id="923f4-131">An Internet connection.</span></span>
* <span data-ttu-id="923f4-132">Een 16 GB of hoger microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="923f4-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="923f4-133">Een USB-SD adapter of microSD-kaart tooburn Hallo besturingssysteeminstallatiekopie op Hallo microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="923f4-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="923f4-134">Een 5-v 2 amp voeding met Hallo 6 mond micro USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="923f4-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="923f4-135">Hallo volgende items zijn optioneel:</span><span class="sxs-lookup"><span data-stu-id="923f4-135">hello following items are optional:</span></span>

* <span data-ttu-id="923f4-136">Een samengesteld Adafruit BME280 temperatuur, druk en vochtigheid sensor.</span><span class="sxs-lookup"><span data-stu-id="923f4-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="923f4-137">Een breadboard.</span><span class="sxs-lookup"><span data-stu-id="923f4-137">A breadboard.</span></span>
* <span data-ttu-id="923f4-138">6 F/M meestal bedrading.</span><span class="sxs-lookup"><span data-stu-id="923f4-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="923f4-139">Een gedempt 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="923f4-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="923f4-140">Deze items zijn optioneel, omdat Hallo code voorbeeld ondersteuning sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="923f4-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="923f4-141">Raspberry Pi instellen</span><span class="sxs-lookup"><span data-stu-id="923f4-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="923f4-142">Hallo Raspbian besturingssysteem voor Pi installeren</span><span class="sxs-lookup"><span data-stu-id="923f4-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="923f4-143">Hallo microSD-kaart voor de installatie van Hallo Raspbian afbeelding voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="923f4-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="923f4-144">Raspbian downloaden.</span><span class="sxs-lookup"><span data-stu-id="923f4-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="923f4-145">[Raspbian Jessie met bureaublad downloaden](https://www.raspberrypi.org/downloads/raspbian/) (Hallo ZIP-bestand).</span><span class="sxs-lookup"><span data-stu-id="923f4-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="923f4-146">Pak Hallo Raspbian installatiekopie tooa map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="923f4-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="923f4-147">Installeer Raspbian toohello microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="923f4-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="923f4-148">[Download en installeer Hallo Etcher SD-kaart brander hulpprogramma](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="923f4-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="923f4-149">Voer Etcher en Hallo Raspbian installatiekopie die u hebt opgehaald in stap 1.</span><span class="sxs-lookup"><span data-stu-id="923f4-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="923f4-150">Selecteer Hallo microSD-kaart station.</span><span class="sxs-lookup"><span data-stu-id="923f4-150">Select hello microSD card drive.</span></span> <span data-ttu-id="923f4-151">Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd Hallo juiste station.</span><span class="sxs-lookup"><span data-stu-id="923f4-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="923f4-152">Klik op Flash tooinstall Raspbian toohello microSD-kaart.</span><span class="sxs-lookup"><span data-stu-id="923f4-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="923f4-153">Hallo microSD-kaart van uw computer verwijderen wanneer de installatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="923f4-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="923f4-154">Het is veilig tooremove hello microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of Hallo microSD-kaart is voltooid ontkoppelt.</span><span class="sxs-lookup"><span data-stu-id="923f4-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="923f4-155">Hallo microSD-kaart invoegen in Pi.</span><span class="sxs-lookup"><span data-stu-id="923f4-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="923f4-156">SSH- en I2C inschakelen</span><span class="sxs-lookup"><span data-stu-id="923f4-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="923f4-157">Sluit Pi toohello monitor, toetsenbord en muis, Pi starten en meld u daarna Raspbian met behulp van `pi` als Hallo-gebruikersnaam en `raspberry` Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="923f4-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="923f4-158">Klik op Hallo Raspberry pictogram > **voorkeuren** > **frambozen Pi configuratie**.</span><span class="sxs-lookup"><span data-stu-id="923f4-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Hallo Raspbian voorkeuren menu](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="923f4-160">Op Hallo **Interfaces** tabblad, stelt u **I2C** en **SSH** te**inschakelen**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="923f4-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="923f4-161">Als u geen fysieke sensoren hebben en sensorgegevens toouse gesimuleerde wilt, moet deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="923f4-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="923f4-163">tooenable SSH en I2C u meer verwijzing documenten vindt op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="923f4-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="923f4-164">Hallo sensor tooPi verbinding</span><span class="sxs-lookup"><span data-stu-id="923f4-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="923f4-165">Hallo breadboard en meestal kabels tooconnect een LED en een tooPi BME280 als volgt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="923f4-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="923f4-166">Als u geen Hallo sensor, [deze sectie overslaan](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="923f4-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hallo frambozen Pi en sensor verbinding](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="923f4-168">Hallo BME280 sensor kunt temperatuur en vochtigheid gegevens verzamelen.</span><span class="sxs-lookup"><span data-stu-id="923f4-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="923f4-169">En Hallo LED knippert als er een communicatie tussen apparaten en Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="923f4-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="923f4-170">Gebruik voor pincodes sensor, Hallo bedrading te volgen:</span><span class="sxs-lookup"><span data-stu-id="923f4-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="923f4-171">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="923f4-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="923f4-172">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="923f4-172">End (Board)</span></span>            | <span data-ttu-id="923f4-173">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="923f4-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="923f4-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="923f4-175">3, 3v PWR (pincode 1)</span><span class="sxs-lookup"><span data-stu-id="923f4-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="923f4-176">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-176">White cable</span></span>   |
| <span data-ttu-id="923f4-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="923f4-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="923f4-178">GND (pincode 6)</span><span class="sxs-lookup"><span data-stu-id="923f4-178">GND (Pin 6)</span></span>            | <span data-ttu-id="923f4-179">Bruine-kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-179">Brown cable</span></span>   |
| <span data-ttu-id="923f4-180">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="923f4-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="923f4-181">I2C1 SDA (pincode 3)</span><span class="sxs-lookup"><span data-stu-id="923f4-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="923f4-182">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-182">Red cable</span></span>     |
| <span data-ttu-id="923f4-183">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="923f4-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="923f4-184">I2C1 SCL (pincode 5)</span><span class="sxs-lookup"><span data-stu-id="923f4-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="923f4-185">Oranje-kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-185">Orange cable</span></span>  |
| <span data-ttu-id="923f4-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="923f4-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="923f4-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="923f4-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="923f4-188">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-188">White cable</span></span>   |
| <span data-ttu-id="923f4-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="923f4-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="923f4-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="923f4-190">GND (Pin 20)</span></span>           | <span data-ttu-id="923f4-191">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="923f4-191">Black cable</span></span>   |

<span data-ttu-id="923f4-192">Klik op tooview [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.</span><span class="sxs-lookup"><span data-stu-id="923f4-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="923f4-193">Nadat u verbinding hebt gemaakt BME280 tooyour frambozen Pi, moet zoals hieronder installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="923f4-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="923f4-195">Pi toohello netwerk verbinden</span><span class="sxs-lookup"><span data-stu-id="923f4-195">Connect Pi toohello network</span></span>

<span data-ttu-id="923f4-196">Pi inschakelen met behulp van Hallo micro USB-kabel en Hallo voeding.</span><span class="sxs-lookup"><span data-stu-id="923f4-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="923f4-197">Gebruik Hallo Ethernet-kabel tooconnect Pi tooyour bekabelde netwerk of volgen Hallo [instructies uit Hallo frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour draadloos netwerk.</span><span class="sxs-lookup"><span data-stu-id="923f4-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="923f4-198">Nadat uw Pi met succes verbonden toohello netwerk is, moet u een notitie van Hallo tootake [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="923f4-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired verbonden netwerk](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="923f4-200">Zorg ervoor dat Pi verbonden toohello netwerk als de computer is.</span><span class="sxs-lookup"><span data-stu-id="923f4-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="923f4-201">Bijvoorbeeld, als uw computer verbonden tooa draadloze netwerk is wanneer Pi verbonden tooa standaardnetwerk is, ziet u mogelijk niet Hallo IP-adres in Hallo devdisco uitvoer.</span><span class="sxs-lookup"><span data-stu-id="923f4-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="923f4-202">Een voorbeeld van een toepassing uitvoeren op Pi</span><span class="sxs-lookup"><span data-stu-id="923f4-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="923f4-203">Klonen van de voorbeeldtoepassing en vereiste hello-pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="923f4-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="923f4-204">Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour frambozen Pi Hallo.</span><span class="sxs-lookup"><span data-stu-id="923f4-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="923f4-205">**Windows-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="923f4-205">**Windows Users**</span></span>
   1. <span data-ttu-id="923f4-206">Download en installeer [PuTTY](http://www.putty.org/) voor Windows.</span><span class="sxs-lookup"><span data-stu-id="923f4-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="923f4-207">Kopieer Hallo IP-adres van de sectie Pi in Hallo Host name (of IP-adres) en selecteer SSH als Hallo verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="923f4-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="923f4-209">**Mac- en Ubuntu-gebruikers**</span><span class="sxs-lookup"><span data-stu-id="923f4-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="923f4-210">Hallo ingebouwde SSH-client op Ubuntu- of Mac OS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="923f4-210">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="923f4-211">Mogelijk moet u toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="923f4-211">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="923f4-212">Hallo standaardgebruikersnaam `pi` , en het Hallo-wachtwoord is `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="923f4-212">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="923f4-213">Installeer Node.js en NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="923f4-213">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="923f4-214">Controleer uw Node.js-versie moet u eerst met de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="923f4-214">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="923f4-215">Of er is geen Node.js op uw Pi Hallo versie lager is dan 4.x uitvoeren na de opdracht tooinstall Hallo of bijwerken van Node.js.</span><span class="sxs-lookup"><span data-stu-id="923f4-215">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="923f4-216">Hallo-voorbeeldtoepassing door het uitvoeren van de volgende opdracht Hallo klonen:</span><span class="sxs-lookup"><span data-stu-id="923f4-216">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="923f4-217">Installeer alle pakketten met Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="923f4-217">Install all packages by hello following command.</span></span> <span data-ttu-id="923f4-218">Omvat Azure IoT-device SDK, BME280 Sensor-bibliotheek en bedrading Pi-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="923f4-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="923f4-219">Het duurt enkele minuten toofinish dit installatieproces, afhankelijk van uw netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="923f4-219">It might take several minutes toofinish this installation process depending on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="923f4-220">Hallo-voorbeeldtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="923f4-220">Configure hello sample application</span></span>

1. <span data-ttu-id="923f4-221">Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="923f4-221">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Configuratiebestand](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="923f4-223">Er zijn twee items in dit bestand kunt u configurate.</span><span class="sxs-lookup"><span data-stu-id="923f4-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="923f4-224">Hallo eerst een is `interval`, definieert een Hallo tijdsinterval (in milliseconden) tussen twee berichten die toocloud verzenden.</span><span class="sxs-lookup"><span data-stu-id="923f4-224">hello first one is `interval`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="923f4-225">tweede Hallo `simulatedData`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="923f4-225">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="923f4-226">Als u **geen Hallo sensor**stelt hello `simulatedData` waarde te`true` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="923f4-226">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="923f4-227">Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="923f4-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="923f4-228">Hallo-voorbeeldtoepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="923f4-228">Run hello sample application</span></span>

<span data-ttu-id="923f4-229">Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="923f4-229">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="923f4-230">Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="923f4-230">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="923f4-231">U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="923f4-231">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Output - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="923f4-233">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="923f4-233">Next steps</span></span>

<span data-ttu-id="923f4-234">U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="923f4-234">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="923f4-235">toosee Hallo-berichten dat uw Pi frambozen tooyour IoT-hub of verzenden berichten tooyour frambozen Pi heeft verzonden in een opdrachtregelinterface Zie Hallo [beheren cloud apparaat messaging met iothub explorer zelfstudie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="923f4-235">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
