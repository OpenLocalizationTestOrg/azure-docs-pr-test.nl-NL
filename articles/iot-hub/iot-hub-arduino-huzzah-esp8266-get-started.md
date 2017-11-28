---
title: aaaESP8266 toocloud - verbinding Doezelaar HUZZAH ESP8266 tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding Adafruit Doezelaar HUZZAH ESP8266 tooAzure IoT Hub voor toosend gegevens toohello Azure cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="2444e-103">Verbinding maken met Adafruit Doezelaar HUZZAH ESP8266 tooAzure IoT-Hub in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="2444e-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Verbinding tussen DHT22 Doezelaar HUZZAH ESP8266 en IoT-Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="2444e-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2444e-105">What you do</span></span>


<span data-ttu-id="2444e-106">Verbinding maken met Adafruit Doezelaar HUZZAH ESP8266 tooan IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="2444e-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="2444e-107">Vervolgens voert u een voorbeeld van toepassing op ESP8266 toocollect Hallo temperatuur en vochtigheid gegevens van een sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="2444e-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="2444e-108">Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="2444e-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2444e-109">Als u andere boards ESP8266 gebruikt, kunt u nog steeds de tooconnect van deze stappen volgen het tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2444e-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="2444e-110">Afhankelijk van het mededelingenbord Hallo ESP8266 u gebruikt, moet u mogelijk tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="2444e-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="2444e-111">Bijvoorbeeld, als u ESP8266 van AI-Thinker, u wijzigt in `0` te`2`.</span><span class="sxs-lookup"><span data-stu-id="2444e-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="2444e-112">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="2444e-112">Don't have a kit yet?</span></span> <span data-ttu-id="2444e-113">Het ophalen van Hallo [Azure-website](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="2444e-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="2444e-114">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2444e-114">What you learn</span></span>

* <span data-ttu-id="2444e-115">Hoe toocreate een IoT-hub en een apparaat registreren voor Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="2444e-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="2444e-116">Hoe tooconnect Doezelaar HUZZAH ESP8266 met Hallo sensoren en uw computer</span><span class="sxs-lookup"><span data-stu-id="2444e-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="2444e-117">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="2444e-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="2444e-118">Hoe toosend Hallo sensor gegevens tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="2444e-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2444e-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2444e-119">What you need</span></span>

![Onderdelen die nodig zijn voor Hallo-zelfstudie](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="2444e-121">toocomplete deze bewerking moet u volgende onderdelen van uw Doezelaar HUZZAH ESP8266 Starter Kit Hallo:</span><span class="sxs-lookup"><span data-stu-id="2444e-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="2444e-122">Hallo Doezelaar HUZZAH ESP8266 mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="2444e-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="2444e-123">Een USB-Micro tooType een USB-kabel</span><span class="sxs-lookup"><span data-stu-id="2444e-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="2444e-124">U moet ook Hallo dingen voor uw ontwikkelomgeving te volgen:</span><span class="sxs-lookup"><span data-stu-id="2444e-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="2444e-125">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2444e-125">An active Azure subscription.</span></span> <span data-ttu-id="2444e-126">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="2444e-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2444e-127">Mac of PC met Windows of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2444e-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="2444e-128">Doezelaar HUZZAH ESP8266 tooconnect voor draadloos netwerk.</span><span class="sxs-lookup"><span data-stu-id="2444e-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="2444e-129">Internet verbinding toodownload Hallo-configuratiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="2444e-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="2444e-130">[Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2444e-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="2444e-131">Eerdere versies werken niet met Hallo AzureIoT-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="2444e-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="2444e-132">Hallo zijn volgende items optioneel als u een sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="2444e-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="2444e-133">U hebt ook Hallo-optie van het gebruik van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="2444e-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="2444e-134">Een Adafruit DHT22 temperatuur en vochtigheid-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="2444e-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="2444e-135">Een breadboard</span><span class="sxs-lookup"><span data-stu-id="2444e-135">A breadboard</span></span>
* <span data-ttu-id="2444e-136">M/M meestal kabels</span><span class="sxs-lookup"><span data-stu-id="2444e-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="2444e-137">Verbinding maken met Doezelaar HUZZAH ESP8266 met Hallo sensoren en uw computer</span><span class="sxs-lookup"><span data-stu-id="2444e-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="2444e-138">In deze sectie maakt verbinding u Hallo sensoren tooyour mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="2444e-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="2444e-139">U sluit uw apparaat tooyour computer voor verdere gebruik.</span><span class="sxs-lookup"><span data-stu-id="2444e-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="2444e-140">Verbinding maken met een DHT22 temperatuur en vochtigheid sensor tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="2444e-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="2444e-141">Hallo breadboard en meestal kabels toomake Hallo verbinding als volgt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2444e-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="2444e-142">Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2444e-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Verbindingen verwijzing](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="2444e-144">Gebruik voor pincodes sensor, Hallo bedrading te volgen:</span><span class="sxs-lookup"><span data-stu-id="2444e-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="2444e-145">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="2444e-145">Start (Sensor)</span></span>           | <span data-ttu-id="2444e-146">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="2444e-146">End (Board)</span></span>           | <span data-ttu-id="2444e-147">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="2444e-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2444e-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="2444e-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="2444e-149">3v (vastmaken 58H)</span><span class="sxs-lookup"><span data-stu-id="2444e-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="2444e-150">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="2444e-150">Red cable</span></span>     |
| <span data-ttu-id="2444e-151">GEGEVENS (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="2444e-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="2444e-152">GPIO 2 (Pin 46)</span><span class="sxs-lookup"><span data-stu-id="2444e-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="2444e-153">Blauw-kabel</span><span class="sxs-lookup"><span data-stu-id="2444e-153">Blue cable</span></span>    |
| <span data-ttu-id="2444e-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="2444e-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="2444e-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="2444e-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="2444e-156">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="2444e-156">Black cable</span></span>   |

<span data-ttu-id="2444e-157">Zie voor meer informatie [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) en [Adafruit Doezelaar HUZZAH Esp8266 pin-outs gegeven](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="2444e-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="2444e-158">Nu moeten uw Doezelaar Huzzah ESP8266 zijn verbonden met een sensor werken.</span><span class="sxs-lookup"><span data-stu-id="2444e-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![DHT22 verbinden met Doezelaar Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="2444e-160">Verbind Doezelaar HUZZAH ESP8266 tooyour computer</span><span class="sxs-lookup"><span data-stu-id="2444e-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="2444e-161">Zoals u volgende, Hallo Micro USB tooType een USB-kabel tooconnect Doezelaar HUZZAH ESP8266 tooyour computer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2444e-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Verbind Doezelaar Huzzah tooyour computer](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="2444e-163">Machtigingen van de seriële poort (alleen Ubuntu) toevoegen</span><span class="sxs-lookup"><span data-stu-id="2444e-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="2444e-164">Als u Ubuntu gebruikt, moet u Hallo machtigingen toooperate op Hallo USB-poort van Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="2444e-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="2444e-165">machtigingen van de seriële poort tooadd, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2444e-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="2444e-166">Voer Hallo opdrachten op een terminal te volgen:</span><span class="sxs-lookup"><span data-stu-id="2444e-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="2444e-167">Ophalen van een Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2444e-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="2444e-168">CRW-rw---1 hoofdmap uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="2444e-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="2444e-169">CRW-rw---1 hoofdmap bellen xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="2444e-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="2444e-170">U ziet dat in de uitvoer van Hallo `uucp` of `dialout` Hallo groepsnaam eigenaar Hallo USB-poort is.</span><span class="sxs-lookup"><span data-stu-id="2444e-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="2444e-171">Hallo-gebruikersgroep toohello door het uitvoeren van de volgende opdracht Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2444e-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="2444e-172">`<group-owner-name>`Hallo eigenaar groepsnaam die u hebt verkregen is in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="2444e-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="2444e-173">`<username>`uw gebruikersnaam Ubuntu is.</span><span class="sxs-lookup"><span data-stu-id="2444e-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="2444e-174">Meld u af bij Ubuntu en vervolgens opnieuw aan te melden voor Hallo wijziging tooappear.</span><span class="sxs-lookup"><span data-stu-id="2444e-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="2444e-175">Sensorgegevens verzamelen en deze tooyour IoT-hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="2444e-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="2444e-176">In deze sectie die u kunt implementeren en uitvoeren van een voorbeeld van toepassing op Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="2444e-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="2444e-177">Hallo-voorbeeldtoepassing knippert Hallo LED Doezelaar HUZZAH ESP8266 en verzendt Hallo temperatuur en vochtigheid gegevens die worden verzameld van Hallo DHT22 sensor tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2444e-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="2444e-178">Hallo-voorbeeldtoepassing ophalen van GitHub</span><span class="sxs-lookup"><span data-stu-id="2444e-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="2444e-179">Hallo-voorbeeldtoepassing wordt gehost op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2444e-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="2444e-180">Kloon Hallo voorbeeld opslagplaats waarin de voorbeeldtoepassing Hallo vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="2444e-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="2444e-181">tooclone hello voorbeeld opslagplaats als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2444e-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="2444e-182">Open een opdrachtprompt of een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="2444e-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="2444e-183">Ga tooa map waarin u Hallo voorbeeld toepassing toobe opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2444e-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="2444e-184">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2444e-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="2444e-185">Hallo-pakket voor Doezelaar HUZZAH ESP8266 op Hallo Arduino IDE installeren:</span><span class="sxs-lookup"><span data-stu-id="2444e-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="2444e-186">Open Hallo map waarin de voorbeeldtoepassing Hallo is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2444e-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="2444e-187">Hallo app.ino bestand openen in Hallo app map in Hallo Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="2444e-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Hallo-voorbeeldtoepassing in Arduino IDE openen](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="2444e-189">Klik in het Hallo Arduino IDE, op **bestand** > **voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="2444e-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="2444e-190">In Hallo **voorkeuren** dialoogvenster vak, klikt u op Hallo pictogram volgende toohello **extra Boards Manager-URL's** vak.</span><span class="sxs-lookup"><span data-stu-id="2444e-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="2444e-191">Voer in het pop-upvenster hello, Hallo URL te volgen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2444e-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url voor het pakket in Arduino IDE punt tooa](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="2444e-193">In Hallo **voorkeur** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2444e-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="2444e-194">Klik op **extra** > **mededelingenbord** > **Boards Manager**, en zoek vervolgens naar esp8266.</span><span class="sxs-lookup"><span data-stu-id="2444e-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="2444e-195">Boards Manager geeft aan dat ESP8266 met een versie van 2.2.0 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2444e-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Hallo esp8266 pakket is geïnstalleerd](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="2444e-197">Klik op **extra** > **mededelingenbord** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="2444e-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="2444e-198">Vereiste bibliotheken installeren</span><span class="sxs-lookup"><span data-stu-id="2444e-198">Install necessary libraries</span></span>

1. <span data-ttu-id="2444e-199">In Hallo Arduino IDE, klikt u op **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.</span><span class="sxs-lookup"><span data-stu-id="2444e-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="2444e-200">Zoeken naar Hallo bibliotheeknamen, één voor één te volgen.</span><span class="sxs-lookup"><span data-stu-id="2444e-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="2444e-201">Voor elke bibliotheek die u vindt, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="2444e-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="2444e-202">Geen een echte DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="2444e-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="2444e-203">Hallo-voorbeeldtoepassing kunt temperatuur en vochtigheid gegevens simuleren als u een echte DHT22 sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="2444e-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="2444e-204">tooset up Hallo toepassing toouse gesimuleerde voorbeeldgegevens, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2444e-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="2444e-205">Open Hallo `config.h` bestand in Hallo `app` map.</span><span class="sxs-lookup"><span data-stu-id="2444e-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="2444e-206">Zoek Hallo coderegel na en wijzig Hallo-waarde van `false` te`true`:</span><span class="sxs-lookup"><span data-stu-id="2444e-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Toepassing hello-toouse gesimuleerde Voorbeeldgegevens configureren](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="2444e-208">Hallo opslaan met `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="2444e-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="2444e-209">Hallo voorbeeld toepassing tooFeather HUZZAH ESP8266 implementeren</span><span class="sxs-lookup"><span data-stu-id="2444e-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="2444e-210">Klik in het Hallo Arduino IDE, op **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort Hallo voor Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="2444e-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="2444e-211">Klik op **schema** > **uploaden** toobuild en Hallo voorbeeld toepassing tooFeather HUZZAH ESP8266 implementeren.</span><span class="sxs-lookup"><span data-stu-id="2444e-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="2444e-212">Voer uw referenties in</span><span class="sxs-lookup"><span data-stu-id="2444e-212">Enter your credentials</span></span>

<span data-ttu-id="2444e-213">Nadat het Hallo uploaden is voltooid, volgt u deze stappen tooenter uw referenties:</span><span class="sxs-lookup"><span data-stu-id="2444e-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="2444e-214">In Hallo Arduino IDE, klikt u op **extra** > **seriële Monitor**.</span><span class="sxs-lookup"><span data-stu-id="2444e-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="2444e-215">Let op Hallo twee vervolgkeuzelijsten in de rechterbenedenhoek Hallo in Hallo seriële monitor-venster.</span><span class="sxs-lookup"><span data-stu-id="2444e-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="2444e-216">Selecteer **er is geen afsluitende regel** voor Hallo links vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2444e-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="2444e-217">Selecteer **115200 baud** voor Hallo rechts vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2444e-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="2444e-218">Voer in Hallo-invoervak Hallo boven aan het venster seriële monitor Hallo Hallo volgende informatie als u wordt gevraagd tooprovide, en klik vervolgens op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="2444e-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="2444e-219">Wi-Fi-SSID</span><span class="sxs-lookup"><span data-stu-id="2444e-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="2444e-220">Wi-Fi-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="2444e-220">Wi-Fi password</span></span>
   * <span data-ttu-id="2444e-221">Apparaat-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="2444e-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="2444e-222">Hallo referentie-informatie wordt opgeslagen in Hallo EEPROM Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="2444e-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="2444e-223">Als u op de herstelknop Hallo op Hallo Doezelaar HUZZAH ESP8266 mededelingenbord, desgewenst Hallo voorbeeldtoepassing tooerase Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="2444e-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="2444e-224">Voer `Y` toohave Hallo informatie gewist.</span><span class="sxs-lookup"><span data-stu-id="2444e-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="2444e-225">U wordt gevraagd tooprovide Hallo informatie een tweede keer.</span><span class="sxs-lookup"><span data-stu-id="2444e-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="2444e-226">Controleer of de voorbeeldtoepassing Hallo correct wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="2444e-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="2444e-227">Als u ziet Hallo volgende de uitvoer van het venster seriële monitor Hallo en Hallo knipperende LED Doezelaar HUZZAH ESP8266, Hallo voorbeeldtoepassing correct wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2444e-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Uiteindelijke uitvoer Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="2444e-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2444e-229">Next steps</span></span>

<span data-ttu-id="2444e-230">U hebt een Doezelaar HUZZAH ESP8266 tooyour IoT-hub verbonden, en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2444e-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

