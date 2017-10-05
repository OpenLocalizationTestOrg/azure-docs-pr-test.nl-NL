---
title: ESP8266 naar cloud - Doezelaar HUZZAH ESP8266 verbinden met Azure IoT Hub | Microsoft Docs
description: Informatie over het instellen en Adafruit Doezelaar HUZZAH ESP8266 verbinden met Azure IoT Hub voor gegevens verzenden naar het Azure-cloud-platform in deze zelfstudie.
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
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="11929-103">Adafruit Doezelaar HUZZAH ESP8266 verbinden met Azure IoT Hub in de cloud</span><span class="sxs-lookup"><span data-stu-id="11929-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Verbinding tussen DHT22 Doezelaar HUZZAH ESP8266 en IoT-Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="11929-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="11929-105">What you do</span></span>


<span data-ttu-id="11929-106">Verbinding maken met Adafruit Doezelaar HUZZAH ESP8266 naar een IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="11929-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="11929-107">Vervolgens voert u een voorbeeld van toepassing op ESP8266 de temperatuur en vochtigheid om gegevens te verzamelen van een sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="11929-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="11929-108">U kunt ten slotte de sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="11929-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="11929-109">Als u andere boards ESP8266 gebruikt, kunt u deze stappen om te verbinden met uw IoT-hub nog steeds volgen.</span><span class="sxs-lookup"><span data-stu-id="11929-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="11929-110">Afhankelijk van de ESP8266 bestuur u gebruikt, moet u mogelijk opnieuw configureren de `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="11929-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="11929-111">Bijvoorbeeld, als u ESP8266 van AI-Thinker, u wijzigt in `0` naar `2`.</span><span class="sxs-lookup"><span data-stu-id="11929-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="11929-112">Heb je nog een kit?</span><span class="sxs-lookup"><span data-stu-id="11929-112">Don't have a kit yet?</span></span> <span data-ttu-id="11929-113">Ophalen van de [Azure-website](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="11929-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="11929-114">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="11929-114">What you learn</span></span>

* <span data-ttu-id="11929-115">Het maken van een IoT-hub en een apparaat registreren voor Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="11929-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="11929-116">Hoe Doezelaar HUZZAH ESP8266 verbinding met de sensor en uw computer</span><span class="sxs-lookup"><span data-stu-id="11929-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="11929-117">Het verzamelen van sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="11929-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="11929-118">Hoe de sensorgegevens verzendt naar uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="11929-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="11929-119">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="11929-119">What you need</span></span>

![Onderdelen die nodig zijn voor de zelfstudie](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="11929-121">Om deze bewerking niet voltooien, moet u de volgende onderdelen van uw Doezelaar HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="11929-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="11929-122">De doezelaar HUZZAH ESP8266-kaart</span><span class="sxs-lookup"><span data-stu-id="11929-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="11929-123">Een Micro USB-Type A USB-kabel</span><span class="sxs-lookup"><span data-stu-id="11929-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="11929-124">U moet ook de volgende bewerkingen voor uw ontwikkelomgeving:</span><span class="sxs-lookup"><span data-stu-id="11929-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="11929-125">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="11929-125">An active Azure subscription.</span></span> <span data-ttu-id="11929-126">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="11929-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="11929-127">Mac of PC met Windows of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="11929-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="11929-128">Doezelaar HUZZAH ESP8266 verbinding maken met draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="11929-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="11929-129">Internet-verbinding voor het downloaden van het hulpprogramma voor serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="11929-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="11929-130">[Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="11929-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="11929-131">Eerdere versies werkt niet met de AzureIoT-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="11929-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="11929-132">De volgende items zijn optioneel als u een sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="11929-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="11929-133">U hebt ook de optie van het gebruik van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="11929-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="11929-134">Een Adafruit DHT22 temperatuur en vochtigheid-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="11929-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="11929-135">Een breadboard</span><span class="sxs-lookup"><span data-stu-id="11929-135">A breadboard</span></span>
* <span data-ttu-id="11929-136">M/M meestal kabels</span><span class="sxs-lookup"><span data-stu-id="11929-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="11929-137">Doezelaar HUZZAH ESP8266 verbinden met de sensor en uw computer</span><span class="sxs-lookup"><span data-stu-id="11929-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="11929-138">In deze sectie kunt u de sensoren verbinding met het mededelingenbord.</span><span class="sxs-lookup"><span data-stu-id="11929-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="11929-139">Vervolgens aansluit u uw apparaat op uw computer voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="11929-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="11929-140">Verbinding maken met een DHT22 temperatuur en vochtigheid sensor Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="11929-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="11929-141">Gebruik de bedrading breadboard en meestal als volgt verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="11929-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="11929-142">Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="11929-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Verbindingen verwijzing](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="11929-144">Gebruik de volgende bedrading voor sensor-pincodes:</span><span class="sxs-lookup"><span data-stu-id="11929-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="11929-145">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="11929-145">Start (Sensor)</span></span>           | <span data-ttu-id="11929-146">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="11929-146">End (Board)</span></span>           | <span data-ttu-id="11929-147">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="11929-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="11929-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="11929-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="11929-149">3v (vastmaken 58H)</span><span class="sxs-lookup"><span data-stu-id="11929-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="11929-150">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="11929-150">Red cable</span></span>     |
| <span data-ttu-id="11929-151">GEGEVENS (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="11929-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="11929-152">GPIO 2 (Pin 46)</span><span class="sxs-lookup"><span data-stu-id="11929-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="11929-153">Blauw-kabel</span><span class="sxs-lookup"><span data-stu-id="11929-153">Blue cable</span></span>    |
| <span data-ttu-id="11929-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="11929-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="11929-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="11929-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="11929-156">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="11929-156">Black cable</span></span>   |

<span data-ttu-id="11929-157">Zie voor meer informatie [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) en [Adafruit Doezelaar HUZZAH Esp8266 pin-outs gegeven](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="11929-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="11929-158">Nu moeten uw Doezelaar Huzzah ESP8266 zijn verbonden met een sensor werken.</span><span class="sxs-lookup"><span data-stu-id="11929-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![DHT22 verbinden met Doezelaar Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="11929-160">Doezelaar HUZZAH ESP8266 aansluiten op uw computer</span><span class="sxs-lookup"><span data-stu-id="11929-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="11929-161">Zoals u volgende, gebruikt u de USB Micro naar Type een USB-kabel Doezelaar HUZZAH ESP8266 aansluiten op uw computer.</span><span class="sxs-lookup"><span data-stu-id="11929-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Doezelaar Huzzah aansluiten op uw computer](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="11929-163">Machtigingen van de seriële poort (alleen Ubuntu) toevoegen</span><span class="sxs-lookup"><span data-stu-id="11929-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="11929-164">Als u Ubuntu gebruikt, zorg er dan voor dat u gemachtigd bent om te werken op de USB-poort van Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="11929-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="11929-165">Als u wilt toevoegen seriële poort machtigingen, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="11929-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="11929-166">Voer de volgende opdrachten in een terminal:</span><span class="sxs-lookup"><span data-stu-id="11929-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="11929-167">U kunt een van de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11929-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="11929-168">CRW-rw---1 hoofdmap uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="11929-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="11929-169">CRW-rw---1 hoofdmap bellen xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="11929-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="11929-170">U ziet dat in de uitvoer `uucp` of `dialout` is de naam van de eigenaar van de USB-poort.</span><span class="sxs-lookup"><span data-stu-id="11929-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="11929-171">De gebruiker toevoegen aan de groep met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="11929-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="11929-172">`<group-owner-name>`is de naam van de eigenaar die u in de vorige stap hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="11929-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="11929-173">`<username>`uw gebruikersnaam Ubuntu is.</span><span class="sxs-lookup"><span data-stu-id="11929-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="11929-174">Meld u af bij Ubuntu en vervolgens opnieuw aan te melden om de wijziging moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="11929-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="11929-175">Sensorgegevens verzamelen en verzenden naar uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="11929-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="11929-176">In deze sectie die u kunt implementeren en uitvoeren van een voorbeeld van toepassing op Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="11929-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="11929-177">De voorbeeldtoepassing de LED Doezelaar HUZZAH ESP8266 knippert en verzendt de temperatuur en vochtigheid gegevens verzameld van de sensor DHT22 naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="11929-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="11929-178">Ophalen van de voorbeeldtoepassing uit GitHub</span><span class="sxs-lookup"><span data-stu-id="11929-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="11929-179">De voorbeeldtoepassing wordt gehost op GitHub.</span><span class="sxs-lookup"><span data-stu-id="11929-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="11929-180">Kloon de opslagplaats voorbeeld waarin de voorbeeldtoepassing vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="11929-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="11929-181">De voorbeeld-opslagplaats klonen, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="11929-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="11929-182">Open een opdrachtprompt of een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="11929-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="11929-183">Ga naar een map waar u de voorbeeldtoepassing moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="11929-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="11929-184">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="11929-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="11929-185">Installeer het pakket voor Doezelaar HUZZAH ESP8266 in Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="11929-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="11929-186">Open de map waar de voorbeeldtoepassing wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="11929-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="11929-187">Open het bestand app.ino in de map van de app in de Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="11929-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![De voorbeeldtoepassing in Arduino IDE openen](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="11929-189">Klik in de IDE Arduino **bestand** > **voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="11929-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="11929-190">In de **voorkeuren** dialoogvenster vak, klik op het pictogram naast de **extra Boards Manager-URL's** vak.</span><span class="sxs-lookup"><span data-stu-id="11929-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="11929-191">Voer de volgende URL in het pop-upvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="11929-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Wijs de url van een pakket in Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="11929-193">In de **voorkeur** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="11929-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="11929-194">Klik op **extra** > **mededelingenbord** > **Boards Manager**, en zoek vervolgens naar esp8266.</span><span class="sxs-lookup"><span data-stu-id="11929-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="11929-195">Boards Manager geeft aan dat ESP8266 met een versie van 2.2.0 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="11929-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Het pakket esp8266 is geïnstalleerd](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="11929-197">Klik op **extra** > **mededelingenbord** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="11929-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="11929-198">Vereiste bibliotheken installeren</span><span class="sxs-lookup"><span data-stu-id="11929-198">Install necessary libraries</span></span>

1. <span data-ttu-id="11929-199">Klik in de IDE Arduino **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.</span><span class="sxs-lookup"><span data-stu-id="11929-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="11929-200">Zoeken naar de volgende bibliotheek benoemt één voor één.</span><span class="sxs-lookup"><span data-stu-id="11929-200">Search for the following library names one by one.</span></span> <span data-ttu-id="11929-201">Voor elke bibliotheek die u vindt, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="11929-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="11929-202">Geen een echte DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="11929-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="11929-203">De voorbeeldtoepassing kunt temperatuur en vochtigheid gegevens simuleren als u een echte DHT22 sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="11929-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="11929-204">U stelt de voorbeeldtoepassing gesimuleerde gegevens gebruiken door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="11929-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="11929-205">Open de `config.h` bestand de `app` map.</span><span class="sxs-lookup"><span data-stu-id="11929-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="11929-206">Zoek de volgende regel code en wijzig de waarde van `false` naar `true`:</span><span class="sxs-lookup"><span data-stu-id="11929-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configureren van de voorbeeldtoepassing gesimuleerde gegevens gebruiken](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="11929-208">Sla het bestand met `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="11929-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="11929-209">De voorbeeldtoepassing voor Doezelaar HUZZAH ESP8266 implementeren</span><span class="sxs-lookup"><span data-stu-id="11929-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="11929-210">Klik in de IDE Arduino **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort voor Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="11929-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="11929-211">Klik op **schema** > **uploaden** kunnen bouwen en implementeren van de voorbeeldtoepassing voor Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="11929-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="11929-212">Voer uw referenties in</span><span class="sxs-lookup"><span data-stu-id="11929-212">Enter your credentials</span></span>

<span data-ttu-id="11929-213">Nadat het uploaden voltooid is, voert u deze stappen om uw referenties invoeren:</span><span class="sxs-lookup"><span data-stu-id="11929-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="11929-214">Klik in de IDE Arduino **extra** > **seriële Monitor**.</span><span class="sxs-lookup"><span data-stu-id="11929-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="11929-215">In het venster seriële monitor ziet u de twee lijsten in de vervolgkeuzelijst in de rechterbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="11929-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="11929-216">Selecteer **er is geen afsluitende regel** voor de linker vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="11929-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="11929-217">Selecteer **115200 baud** voor de lijst rechts vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="11929-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="11929-218">Voer de volgende gegevens in het invoervak zich boven aan het venster seriële monitor, als u wordt gevraagd om ze en klik vervolgens op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="11929-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="11929-219">Wi-Fi-SSID</span><span class="sxs-lookup"><span data-stu-id="11929-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="11929-220">Wi-Fi-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="11929-220">Wi-Fi password</span></span>
   * <span data-ttu-id="11929-221">Apparaat-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="11929-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="11929-222">De referentie-informatie wordt opgeslagen in de EEPROM van Doezelaar HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="11929-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="11929-223">Als u op de knop herstellen op het mededelingenbord Doezelaar HUZZAH ESP8266 klikt, wordt de voorbeeldtoepassing gevraagd als u wilt de gegevens wissen.</span><span class="sxs-lookup"><span data-stu-id="11929-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="11929-224">Voer `Y` te beschikken over de gegevens gewist.</span><span class="sxs-lookup"><span data-stu-id="11929-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="11929-225">U wordt gevraagd om de informatie van een tweede keer te geven.</span><span class="sxs-lookup"><span data-stu-id="11929-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="11929-226">Controleer of dat de voorbeeldtoepassing met succes wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="11929-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="11929-227">Als u de volgende uitvoer van het monitorvenster seriële en de knipperende LED op Doezelaar HUZZAH ESP8266 ziet, wordt de voorbeeldtoepassing met succes uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11929-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Uiteindelijke uitvoer Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="11929-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11929-229">Next steps</span></span>

<span data-ttu-id="11929-230">U hebt een Doezelaar HUZZAH ESP8266 verbonden met uw IoT-hub, en de vastgelegde sensorgegevens verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="11929-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

