---
title: aaaESP8266 toocloud - verbinding Sparkfun ESP8266 ding Dev tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding Sparkfun ESP8266 ding Dev tooAzure IoT Hub voor toosend gegevens toohello Azure cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="2ac5d-103">Verbinding maken met Sparkfun ESP8266 ding Dev tooAzure IoT-Hub in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="2ac5d-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![verbinding tussen DHT22, wat Dev en IoT-Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="2ac5d-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2ac5d-105">What you will do</span></span>

<span data-ttu-id="2ac5d-106">Verbinding maken met Sparkfun ESP8266 ding Dev tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="2ac5d-107">Voer vervolgens een voorbeeld van toepassing op ESP8266 toocollect temperatuur en vochtigheid gegevens van een sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="2ac5d-108">Ten slotte verzenden Hallo sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2ac5d-109">Als u andere boards ESP8266 gebruikt, kunt u nog steeds de tooconnect van deze stappen volgen het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="2ac5d-110">Afhankelijk van het mededelingenbord Hallo ESP8266 u gebruikt, moet u mogelijk tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="2ac5d-111">Bijvoorbeeld, als u ESP8266 van AI Thinker gebruikt, u kunt wijzigen in `0` te`2`.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="2ac5d-112">Een kit nog geen hebt?: klik op [hier](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2ac5d-113">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2ac5d-113">What you will learn</span></span>

* <span data-ttu-id="2ac5d-114">Hoe toocreate een IoT-hub en een apparaat registreren voor voor ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2ac5d-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="2ac5d-115">Hoe tooconnect ding Dev met Hallo sensoren en uw computer.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="2ac5d-116">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op wat ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2ac5d-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="2ac5d-117">Hoe Hallo toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="2ac5d-118">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2ac5d-118">What you will need</span></span>

![Onderdelen die nodig zijn voor Hallo-zelfstudie](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="2ac5d-120">toocomplete deze bewerking moet u volgende onderdelen van uw ding Developer Starter Kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="2ac5d-121">Hello Sparkfun ESP8266 ding Dev mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="2ac5d-122">Een USB-Micro tooType een USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="2ac5d-123">U moet ook de volgende Hallo voor uw ontwikkelomgeving:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="2ac5d-124">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-124">An active Azure subscription.</span></span> <span data-ttu-id="2ac5d-125">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2ac5d-126">Mac of PC met Windows of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="2ac5d-127">Sparkfun ESP8266 ding Dev tooconnect voor draadloos netwerk.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="2ac5d-128">Internet verbinding toodownload Hallo-configuratiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="2ac5d-129">[Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 (of nieuwer), eerdere versies werkt niet met Hallo AzureIoT-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="2ac5d-130">Hallo zijn volgende items optioneel als u een sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="2ac5d-131">U hebt ook Hallo-optie van het gebruik van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="2ac5d-132">Een Adafruit DHT22-sensor van temperatuur en vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="2ac5d-133">Een breadboard.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-133">A breadboard.</span></span>
* <span data-ttu-id="2ac5d-134">M/M meestal bedrading.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="2ac5d-135">Verbinding maken met ESP8266 ding Dev met Hallo sensoren en uw computer</span><span class="sxs-lookup"><span data-stu-id="2ac5d-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="2ac5d-136">Verbinding maken met een DHT22 temperatuur en vochtigheid sensor tooESP8266 ding Dev</span><span class="sxs-lookup"><span data-stu-id="2ac5d-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="2ac5d-137">Hallo breadboard en meestal kabels toomake Hallo verbinding als volgt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="2ac5d-138">Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Verbindingen verwijzing](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="2ac5d-140">Voor pincodes sensor, we Hallo bedrading volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="2ac5d-141">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-141">Start (Sensor)</span></span>           | <span data-ttu-id="2ac5d-142">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-142">End (Board)</span></span>           | <span data-ttu-id="2ac5d-143">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="2ac5d-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2ac5d-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="2ac5d-145">3v (8A pincode)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="2ac5d-146">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="2ac5d-146">Red cable</span></span>     |
| <span data-ttu-id="2ac5d-147">GEGEVENS (Pin 28 septies)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="2ac5d-148">GPIO 2 (9A pincode)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="2ac5d-149">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="2ac5d-149">White cable</span></span>    |
| <span data-ttu-id="2ac5d-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="2ac5d-151">GND (7J pincode)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="2ac5d-152">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="2ac5d-152">Black cable</span></span>   |


- <span data-ttu-id="2ac5d-153">Zie voor meer informatie: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) en [Sparkfun ESP8266 ding Dev-specificatie](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="2ac5d-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="2ac5d-154">Nu moeten uw Sparkfun ESP8266 ding Dev zijn verbonden met een sensor werken.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![verbinding maken met dht22 met ESP8266 ding Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="2ac5d-156">Verbind Sparkfun ESP8266 ding Dev tooyour computer</span><span class="sxs-lookup"><span data-stu-id="2ac5d-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="2ac5d-157">Hallo Micro USB tooType een USB-kabel tooconnect Sparkfun ESP8266 ding Dev tooyour computer als volgt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![Verbind Doezelaar huzzah tooyour computer](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="2ac5d-159">Machtigingen van de seriële poort – Ubuntu alleen toevoegen</span><span class="sxs-lookup"><span data-stu-id="2ac5d-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="2ac5d-160">Als u Ubuntu gebruikt, controleert u of dat een normale gebruiker heeft Hallo machtigingen toooperate op Hallo USB-poort van Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2ac5d-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="2ac5d-161">tooadd seriële poort machtigingen voor een normale gebruiker, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="2ac5d-162">Voer Hallo opdrachten op een terminal te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="2ac5d-163">Ophalen van een Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="2ac5d-164">CRW-rw---1 hoofdmap uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="2ac5d-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="2ac5d-165">CRW-rw---1 hoofdmap bellen xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="2ac5d-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="2ac5d-166">In de uitvoer van Hallo kennisgeving `uucp` of `dialout` die Hallo eigenaar groepsnaam Hallo USB-poort.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="2ac5d-167">Hallo-gebruikersgroep toohello door het uitvoeren van de volgende opdracht Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="2ac5d-168">`<group-owner-name>`Hallo eigenaar groepsnaam die u hebt verkregen is in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="2ac5d-169">`<username>`uw gebruikersnaam Ubuntu is.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="2ac5d-170">Ubuntu afmelden en deze opnieuw aanmelden voor Hallo wijziging tootake effect.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="2ac5d-171">Sensorgegevens verzamelen en deze tooyour IoT-hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="2ac5d-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="2ac5d-172">In deze sectie kunt u gegevens kunt implementeren en uitvoeren van een voorbeeldtoepassing op Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2ac5d-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="2ac5d-173">Hallo-voorbeeldtoepassing Hallo LED Sparkfun ESP8266 ding Dev knippert en verzendt Hallo temperatuur en vochtigheid gegevens die worden verzameld van Hallo DHT22 sensor tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="2ac5d-174">Hallo-voorbeeldtoepassing ophalen van GitHub</span><span class="sxs-lookup"><span data-stu-id="2ac5d-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="2ac5d-175">Hallo-voorbeeldtoepassing wordt gehost op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="2ac5d-176">Kloon Hallo voorbeeld opslagplaats waarin de voorbeeldtoepassing Hallo vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="2ac5d-177">tooclone hello voorbeeld opslagplaats als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="2ac5d-178">Open een opdrachtprompt of een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="2ac5d-179">Ga tooa map waarin u Hallo voorbeeld toepassing toobe opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="2ac5d-180">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="2ac5d-181">Hallo-pakket voor Sparkfun ESP8266 ding Dev Arduino IDE installeren:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="2ac5d-182">Open Hallo map waarin de voorbeeldtoepassing Hallo is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="2ac5d-183">Hallo app.ino bestand openen in Hallo app map in Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Hallo-voorbeeldtoepassing in arduino ide openen](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="2ac5d-185">Klik in het Hallo Arduino IDE, op **bestand** > **voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="2ac5d-186">In Hallo **voorkeuren** dialoogvenster vak, klikt u op Hallo pictogram volgende toohello **extra Boards Manager-URL's** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="2ac5d-187">Voer in het pop-upvenster hello, Hallo URL te volgen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url voor het pakket in arduino ide punt tooa](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="2ac5d-189">In Hallo **voorkeur** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="2ac5d-190">Klik op **extra** > **mededelingenbord** > **Boards Manager**, en zoek vervolgens naar esp8266.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="2ac5d-191">ESP8266 met een versie van 2.2.0 of later moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Hallo esp8266 pakket is geïnstalleerd](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="2ac5d-193">Klik op **extra** > **mededelingenbord** > **Sparkfun ESP8266 ding Dev**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="2ac5d-194">Vereiste bibliotheken installeren</span><span class="sxs-lookup"><span data-stu-id="2ac5d-194">Install necessary libraries</span></span>

1. <span data-ttu-id="2ac5d-195">In Hallo Arduino IDE, klikt u op **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="2ac5d-196">Zoeken naar Hallo bibliotheeknamen, één voor één te volgen.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="2ac5d-197">Voor elk Hallo-bibliotheek die u vindt, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="2ac5d-198">Geen een echte DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="2ac5d-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="2ac5d-199">Hallo-voorbeeldtoepassing kunt temperatuur en vochtigheid gegevens simuleren als u een echte DHT22 sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="2ac5d-200">tooenable hello toepassing toouse gesimuleerde voorbeeldgegevens, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="2ac5d-201">Open Hallo `config.h` bestand in Hallo `app` map.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="2ac5d-202">Zoek Hallo coderegel na en wijzig Hallo-waarde van `false` te`true`:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Toepassing hello-toouse gesimuleerde Voorbeeldgegevens configureren](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="2ac5d-204">Sla met `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="2ac5d-205">Hallo voorbeeld toepassing tooSparkfun ESP8266 ding Dev implementeren</span><span class="sxs-lookup"><span data-stu-id="2ac5d-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="2ac5d-206">Klik in het Hallo Arduino IDE, op **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort Hallo voor voor Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2ac5d-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="2ac5d-207">Klik op **schema** > **uploaden** toobuild en Hallo voorbeeld toepassing tooSparkfun ESP8266 ding ontwikkelaars implementeren</span><span class="sxs-lookup"><span data-stu-id="2ac5d-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="2ac5d-208">Als u Mac OS kan er waarschijnlijk Hallo volgende berichten tijdens het uploaden.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="2ac5d-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="2ac5d-210">Open uw ternimal-venster en voltooien hieronder acties toosolve dit probleem.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="2ac5d-211">Voer uw referenties in</span><span class="sxs-lookup"><span data-stu-id="2ac5d-211">Enter your credentials</span></span>

<span data-ttu-id="2ac5d-212">Na het Hallo uploaden is voltooid, voert u Hallo stappen tooenter uw referenties:</span><span class="sxs-lookup"><span data-stu-id="2ac5d-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="2ac5d-213">In Hallo Arduino IDE, klikt u op **extra** > **seriële Monitor**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="2ac5d-214">U ziet Hallo twee vervolgkeuzelijsten op Hallo rechterbenedenhoek in Hallo seriële monitor-venster.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="2ac5d-215">Selecteer **er is geen afsluitende regel** voor Hallo links vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="2ac5d-216">Selecteer **115200 baud** voor Hallo rechts vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="2ac5d-217">Voer in Hallo-invoervak Hallo boven aan het venster seriële monitor Hallo Hallo volgende informatie als u wordt gevraagd tooprovide, en klik vervolgens op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="2ac5d-218">Wi-Fi-SSID</span><span class="sxs-lookup"><span data-stu-id="2ac5d-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="2ac5d-219">Wi-Fi-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="2ac5d-219">Wi-Fi password</span></span>
   * <span data-ttu-id="2ac5d-220">Apparaat-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="2ac5d-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="2ac5d-221">Hallo referentie-informatie wordt opgeslagen in Hallo EEPROM van Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2ac5d-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="2ac5d-222">Als u op de herstelknop Hallo op Hallo Sparkfun ESP8266 ding Dev mededelingenbord, Hallo voorbeeldtoepassing wordt u gevraagd als u wilt dat tooerase Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="2ac5d-223">Voer `Y` toohave Hallo informatie gewist en wordt u gevraagd tooprovide Hallo gegevens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="2ac5d-224">Controleer of de voorbeeldtoepassing Hallo correct wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="2ac5d-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="2ac5d-225">Als u ziet Hallo volgende de uitvoer van het venster seriële monitor Hallo en Hallo knipperende LED Sparkfun ESP8266 ding Dev, Hallo voorbeeldtoepassing correct wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![uiteindelijke uitvoer arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="2ac5d-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ac5d-227">Next steps</span></span>

<span data-ttu-id="2ac5d-228">U hebt een Sparkfun ESP8266 ding Dev tooyour IoT-hub verbonden en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ac5d-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
