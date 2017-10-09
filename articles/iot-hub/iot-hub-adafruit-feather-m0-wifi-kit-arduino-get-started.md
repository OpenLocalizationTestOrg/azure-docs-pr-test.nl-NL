---
title: 'M0 toocloud: verbinding maken met Doezelaar M0 Wi-Fi tooAzure IoT Hub | Microsoft Docs'
description: Meer informatie over hoe tooset boven en verbinding maken met Adafruit Doezelaar M0 Wi-Fi tooAzure IoT Hub toosend gegevens toohello Azure cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="39c2a-103">Verbinding maken met Adafruit Doezelaar M0 Wi-Fi tooAzure IoT-Hub in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="39c2a-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Verbinding tussen een BME280, Doezelaar M0 Wi-Fi en IoT-Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="39c2a-105">In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met het mededelingenbord Arduino leren.</span><span class="sxs-lookup"><span data-stu-id="39c2a-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="39c2a-106">U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="39c2a-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="39c2a-107">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="39c2a-107">What you do</span></span>

<span data-ttu-id="39c2a-108">Verbinding maken met Adafruit Doezelaar M0 Wi-Fi tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="39c2a-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="39c2a-109">Vervolgens voert u een voorbeeld van toepassing op M0 Wi-Fi toocollect Hallo temperatuur en vochtigheid gegevens uit een BME280.</span><span class="sxs-lookup"><span data-stu-id="39c2a-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="39c2a-110">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="39c2a-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="39c2a-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="39c2a-111">What you learn</span></span>

* <span data-ttu-id="39c2a-112">Hoe toocreate een IoT-hub en een apparaat registreren voor Doezelaar M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="39c2a-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="39c2a-113">Hoe tooconnect Doezelaar M0 Wi-Fi met Hallo sensoren en uw computer</span><span class="sxs-lookup"><span data-stu-id="39c2a-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="39c2a-114">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Doezelaar M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="39c2a-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="39c2a-115">Hoe toosend Hallo sensor gegevens tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="39c2a-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="39c2a-116">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="39c2a-116">What you need</span></span>

![Onderdelen die nodig zijn voor Hallo-zelfstudie](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="39c2a-118">toocomplete deze bewerking moet u volgende onderdelen van uw Doezelaar M0 Wi-Fi Starter Kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="39c2a-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="39c2a-119">Hallo Doezelaar M0 Wi-Fi mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="39c2a-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="39c2a-120">Een USB-Micro tooType een USB-kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="39c2a-121">U moet ook Hallo dingen voor uw ontwikkelomgeving te volgen:</span><span class="sxs-lookup"><span data-stu-id="39c2a-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="39c2a-122">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="39c2a-122">An active Azure subscription.</span></span> <span data-ttu-id="39c2a-123">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="39c2a-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="39c2a-124">Een Mac of een PC met Windows of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="39c2a-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="39c2a-125">Een draadloos netwerk voor Doezelaar M0 Wi-Fi-tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="39c2a-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="39c2a-126">Een Internet verbinding toodownload Hallo configuratiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="39c2a-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="39c2a-127">[Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="39c2a-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="39c2a-128">Eerdere versies werken niet met hello Azure IoT Hub-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="39c2a-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="39c2a-129">Als u een sensor hebt, is Hallo volgende items zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="39c2a-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="39c2a-130">U hebt ook een optie van het gebruik van gesimuleerde sensorgegevens Hallo:</span><span class="sxs-lookup"><span data-stu-id="39c2a-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="39c2a-131">Een BME280 temperatuur en vochtigheid sensor</span><span class="sxs-lookup"><span data-stu-id="39c2a-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="39c2a-132">Een breadboard</span><span class="sxs-lookup"><span data-stu-id="39c2a-132">A breadboard</span></span>
* <span data-ttu-id="39c2a-133">M/M meestal kabels</span><span class="sxs-lookup"><span data-stu-id="39c2a-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="39c2a-134">Verbinding maken met Doezelaar M0 Wi-Fi met Hallo sensoren en uw computer</span><span class="sxs-lookup"><span data-stu-id="39c2a-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="39c2a-135">In deze sectie maakt verbinding u Hallo sensoren tooyour mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="39c2a-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="39c2a-136">U sluit uw apparaat tooyour computer voor verdere gebruik.</span><span class="sxs-lookup"><span data-stu-id="39c2a-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="39c2a-137">Verbinding maken met een DHT22 temperatuur en vochtigheid sensor tooFeather M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="39c2a-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="39c2a-138">Hallo breadboard en meestal kabels toomake Hallo verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39c2a-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="39c2a-139">Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39c2a-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Verbindingen verwijzing](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="39c2a-141">Gebruik voor pincodes sensor, Hallo bedrading te volgen:</span><span class="sxs-lookup"><span data-stu-id="39c2a-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="39c2a-142">Start (sensor)</span><span class="sxs-lookup"><span data-stu-id="39c2a-142">Start (sensor)</span></span>           | <span data-ttu-id="39c2a-143">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="39c2a-143">End (board)</span></span>            | <span data-ttu-id="39c2a-144">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="39c2a-145">VDD (Pin 27A)</span><span class="sxs-lookup"><span data-stu-id="39c2a-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="39c2a-146">3v (3A pincode)</span><span class="sxs-lookup"><span data-stu-id="39c2a-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="39c2a-147">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-147">Red cable</span></span>     |
| <span data-ttu-id="39c2a-148">GND (Pin 29 bis)</span><span class="sxs-lookup"><span data-stu-id="39c2a-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="39c2a-149">GND (6A pincode)</span><span class="sxs-lookup"><span data-stu-id="39c2a-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="39c2a-150">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-150">Black cable</span></span>   |
| <span data-ttu-id="39c2a-151">SCK (pincode 30)</span><span class="sxs-lookup"><span data-stu-id="39c2a-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="39c2a-152">SCK (Pin 12A)</span><span class="sxs-lookup"><span data-stu-id="39c2a-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="39c2a-153">Gele-kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-153">Yellow cable</span></span>  |
| <span data-ttu-id="39c2a-154">SDO (Pin 31A)</span><span class="sxs-lookup"><span data-stu-id="39c2a-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="39c2a-155">MI (Pin 14A)</span><span class="sxs-lookup"><span data-stu-id="39c2a-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="39c2a-156">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-156">White cable</span></span>   |
| <span data-ttu-id="39c2a-157">SDI (Pin 32 bis)</span><span class="sxs-lookup"><span data-stu-id="39c2a-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="39c2a-158">M0 (Pin 13A)</span><span class="sxs-lookup"><span data-stu-id="39c2a-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="39c2a-159">Blauw-kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-159">Blue cable</span></span>    |
| <span data-ttu-id="39c2a-160">CS (Pin 33A)</span><span class="sxs-lookup"><span data-stu-id="39c2a-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="39c2a-161">GPIO 5 (Pin 15J)</span><span class="sxs-lookup"><span data-stu-id="39c2a-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="39c2a-162">Oranje-kabel</span><span class="sxs-lookup"><span data-stu-id="39c2a-162">Orange cable</span></span>  |

<span data-ttu-id="39c2a-163">Zie voor meer informatie [Adafruit BME280 vochtigheid + barometerdruk + temperatuur Sensor evenement](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) en [Adafruit Doezelaar M0 Wi-Fi pin-outs gegeven](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="39c2a-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="39c2a-164">Nu moeten uw Doezelaar M0 Wi-Fi zijn verbonden met een sensor werken.</span><span class="sxs-lookup"><span data-stu-id="39c2a-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![DHT22 verbinden met Doezelaar Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="39c2a-166">Verbind Doezelaar M0 Wi-Fi tooyour computer</span><span class="sxs-lookup"><span data-stu-id="39c2a-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="39c2a-167">Hallo Micro USB tooType een USB-kabel tooconnect Doezelaar M0 Wi-Fi tooyour computer gebruiken, zoals wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="39c2a-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Verbind Doezelaar Huzzah tooyour computer](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="39c2a-169">Machtigingen van de seriële poort (alleen Ubuntu) toevoegen</span><span class="sxs-lookup"><span data-stu-id="39c2a-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="39c2a-170">Als u Ubuntu gebruikt, moet u Hallo machtigingen toooperate op Hallo USB-poort van Doezelaar M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="39c2a-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="39c2a-171">machtigingen van de seriële poort tooadd, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="39c2a-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="39c2a-172">Voer op een terminal Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="39c2a-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="39c2a-173">Ophalen van een Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="39c2a-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="39c2a-174">CRW-rw---1 hoofdmap uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="39c2a-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="39c2a-175">CRW-rw---1 hoofdmap bellen xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="39c2a-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="39c2a-176">U ziet dat in de uitvoer van Hallo `uucp` of `dialout` Hallo groepsnaam eigenaar Hallo USB-poort is.</span><span class="sxs-lookup"><span data-stu-id="39c2a-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="39c2a-177">tooadd hello toohello gebruikersgroep, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="39c2a-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="39c2a-178">In de vorige stap hello, die u hebt verkregen Hallo eigenaar groepsnaam `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="39c2a-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="39c2a-179">De gebruikersnaam Ubuntu `<username>`.</span><span class="sxs-lookup"><span data-stu-id="39c2a-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="39c2a-180">Meld u af bij Ubuntu voor Hallo wijziging tooappear, en vervolgens weer aanmelden.</span><span class="sxs-lookup"><span data-stu-id="39c2a-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="39c2a-181">Sensorgegevens verzamelen en deze tooyour IoT-hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="39c2a-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="39c2a-182">In deze sectie die u kunt implementeren en uitvoeren van een voorbeeld van toepassing op Doezelaar M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="39c2a-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="39c2a-183">Hallo-voorbeeldtoepassing maakt Hallo LED knipperen aan Doezelaar M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="39c2a-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="39c2a-184">Verzendt vervolgens Hallo temperatuur en vochtigheid gegevens die worden verzameld van Hallo BME280 sensor tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="39c2a-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="39c2a-185">Hallo-voorbeeldtoepassing ophalen van GitHub en Hallo Arduino IDE voorbereiden</span><span class="sxs-lookup"><span data-stu-id="39c2a-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="39c2a-186">Hallo-voorbeeldtoepassing wordt gehost op GitHub.</span><span class="sxs-lookup"><span data-stu-id="39c2a-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="39c2a-187">Kloon Hallo voorbeeld opslagplaats waarin de voorbeeldtoepassing Hallo vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="39c2a-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="39c2a-188">tooclone hello voorbeeld opslagplaats als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="39c2a-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="39c2a-189">Open een opdrachtprompt of een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="39c2a-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="39c2a-190">Ga tooa map waarin u Hallo voorbeeld toepassing toobe opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="39c2a-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="39c2a-191">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="39c2a-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="39c2a-192">Hallo-pakket voor Doezelaar M0 Wi-Fi in Hallo Arduino IDE installeren</span><span class="sxs-lookup"><span data-stu-id="39c2a-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="39c2a-193">Open Hallo map waarin de voorbeeldtoepassing Hallo is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="39c2a-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="39c2a-194">Hallo app.ino bestand openen in Hallo app map in Hallo Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="39c2a-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Hallo-voorbeeldtoepassing in Arduino IDE openen](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="39c2a-196">Klik op **bestand** > **voorkeuren** (Windows of Linux) of **Arduino** > **voorkeuren** (Mac) en kopieert en koppeling hieronder Hallo in Hallo plakken **extra Boards Manager-URL's** optie in Hallo Arduino IDE-voorkeuren.</span><span class="sxs-lookup"><span data-stu-id="39c2a-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="39c2a-197">Klik op **extra** > **mededelingenbord** > **Boards Manager**, en installeer vervolgens Hallo `Arduino SAMD Boards` versie `1.6.2` of hoger.</span><span class="sxs-lookup"><span data-stu-id="39c2a-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="39c2a-198">Klik dan in hetzelfde venster hello, installeert u `Adafruit SAMD Boards` tooadd Hallo mededelingenbord bestand definities van het pakket.</span><span class="sxs-lookup"><span data-stu-id="39c2a-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![Hallo esp8266 pakket is geïnstalleerd](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="39c2a-200">Klik op **extra** > **mededelingenbord** > **Adafruit M0 Wi-Fi**.</span><span class="sxs-lookup"><span data-stu-id="39c2a-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="39c2a-201">Stuurprogramma's installeren (voor Windows).</span><span class="sxs-lookup"><span data-stu-id="39c2a-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="39c2a-202">Wanneer u Doezelaar M0 Wi-Fi aansluit, moet u mogelijk een stuurprogramma tooinstall.</span><span class="sxs-lookup"><span data-stu-id="39c2a-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="39c2a-203">Klik op [Hallo downloadkoppeling op Hallo webpagina](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload Hallo stuurprogramma installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="39c2a-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="39c2a-204">Ga als volgt Hallo stappen tooinstall Hallo stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="39c2a-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="39c2a-205">Vereiste bibliotheken installeren</span><span class="sxs-lookup"><span data-stu-id="39c2a-205">Install necessary libraries</span></span>

1. <span data-ttu-id="39c2a-206">In Hallo Arduino IDE, klikt u op **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.</span><span class="sxs-lookup"><span data-stu-id="39c2a-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="39c2a-207">Zoeken naar Hallo bibliotheeknamen, één voor één te volgen.</span><span class="sxs-lookup"><span data-stu-id="39c2a-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="39c2a-208">Voor elke bibliotheek die u vindt, klikt u op **installeren**:</span><span class="sxs-lookup"><span data-stu-id="39c2a-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="39c2a-209">Handmatig installeren `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="39c2a-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="39c2a-210">Ga te[deze website](https://github.com/adafruit/Adafruit_WINC1500) en klik op **klonen of downloaden** > **ZIP downloaden**.</span><span class="sxs-lookup"><span data-stu-id="39c2a-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="39c2a-211">In uw IDE Arduino gaat te**schema** > **bibliotheek omvatten** > **.zip bibliotheek toevoegen** en Hallo zip-bestand toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="39c2a-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="39c2a-212">Hallo-voorbeeldtoepassing gebruiken als u een echte BME280-temperatuursensor hebt</span><span class="sxs-lookup"><span data-stu-id="39c2a-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="39c2a-213">Als u een echte BME280 sensor geen hebt, kunt de voorbeeldtoepassing Hallo temperatuur en vochtigheid gegevens simuleren.</span><span class="sxs-lookup"><span data-stu-id="39c2a-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="39c2a-214">tooset up Hallo toepassing toouse gesimuleerde voorbeeldgegevens, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="39c2a-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="39c2a-215">Open Hallo `config.h` bestand in Hallo `app` map.</span><span class="sxs-lookup"><span data-stu-id="39c2a-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="39c2a-216">Zoek Hallo coderegel na en wijzig Hallo-waarde van `false` te`true`:</span><span class="sxs-lookup"><span data-stu-id="39c2a-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Toepassing hello-toouse gesimuleerde Voorbeeldgegevens configureren](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="39c2a-218">Hallo opslaan met `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="39c2a-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="39c2a-219">Hallo voorbeeld toepassing tooFeather M0 Wi-Fi implementeren</span><span class="sxs-lookup"><span data-stu-id="39c2a-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="39c2a-220">Klik in het Hallo Arduino IDE, op **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort Hallo voor Doezelaar M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="39c2a-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="39c2a-221">Klik op **schema** > **uploaden** toobuild en Hallo voorbeeld toepassing tooFeather M0 Wi-Fi implementeren.</span><span class="sxs-lookup"><span data-stu-id="39c2a-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="39c2a-222">Voer uw referenties in</span><span class="sxs-lookup"><span data-stu-id="39c2a-222">Enter your credentials</span></span>

<span data-ttu-id="39c2a-223">Nadat het Hallo uploaden is voltooid, volgt u deze stappen tooenter uw referenties:</span><span class="sxs-lookup"><span data-stu-id="39c2a-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="39c2a-224">In Hallo Arduino IDE, klikt u op **extra** > **seriële Monitor**.</span><span class="sxs-lookup"><span data-stu-id="39c2a-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="39c2a-225">Selecteer in de Hallo rechterbenedenhoek van het venster seriële monitor Hallo, **er is geen afsluitende regel** in Hallo vervolgkeuzelijst aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="39c2a-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="39c2a-226">Selecteer **115200 baud** in Hallo vervolgkeuzelijst op de juiste Hallo.</span><span class="sxs-lookup"><span data-stu-id="39c2a-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="39c2a-227">Voer in invoervak Hallo Hallo boven Hallo volgende informatie als u bent tooprovide gevraagd en klik op **verzenden**:</span><span class="sxs-lookup"><span data-stu-id="39c2a-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="39c2a-228">Wi-Fi-SSID</span><span class="sxs-lookup"><span data-stu-id="39c2a-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="39c2a-229">Wi-Fi-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="39c2a-229">Wi-Fi password</span></span>
   * <span data-ttu-id="39c2a-230">Apparaat-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="39c2a-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="39c2a-231">Hallo referentie-informatie wordt opgeslagen in Hallo EEPROM Doezelaar M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="39c2a-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="39c2a-232">Als u op de herstelknop Hallo op Hallo mededelingenbord Doezelaar M0 Wi-Fi, desgewenst Hallo voorbeeldtoepassing tooerase Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="39c2a-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="39c2a-233">Voer `Y` tooerase Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="39c2a-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="39c2a-234">U wordt gevraagd tooprovide Hallo informatie een tweede keer.</span><span class="sxs-lookup"><span data-stu-id="39c2a-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="39c2a-235">Controleren of de voorbeeldtoepassing Hallo met succes wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="39c2a-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="39c2a-236">Als u ziet Hallo volgende de uitvoer van het venster seriële monitor Hallo en Hallo knipperende LED Doezelaar M0 Wi-Fi, Hallo voorbeeldtoepassing correct wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="39c2a-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Uiteindelijke uitvoer Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="39c2a-238">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39c2a-238">Next steps</span></span>

<span data-ttu-id="39c2a-239">U hebt verbonden Doezelaar M0 Wi-Fi tooyour IoT-hub en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="39c2a-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

