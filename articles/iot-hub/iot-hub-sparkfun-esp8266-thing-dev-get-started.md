---
title: ESP8266 naar cloud - Sparkfun ESP8266 ding Dev verbinding maken met Azure IoT Hub | Microsoft Docs
description: Informatie over het instellen en Sparkfun ESP8266 ding Dev verbinden met Azure IoT Hub voor gegevens verzenden naar het Azure-cloud-platform in deze zelfstudie.
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
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="2772f-103">Sparkfun ESP8266 ding Dev verbinden met Azure IoT Hub in de cloud</span><span class="sxs-lookup"><span data-stu-id="2772f-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![verbinding tussen DHT22, wat Dev en IoT-Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="2772f-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2772f-105">What you will do</span></span>

<span data-ttu-id="2772f-106">Verbinding maken met Sparkfun ESP8266 ding Dev naar een IoT-hub die u maakt.</span><span class="sxs-lookup"><span data-stu-id="2772f-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="2772f-107">Voer vervolgens een voorbeeld van toepassing op ESP8266 temperatuur en vochtigheid om gegevens te verzamelen van een sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="2772f-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="2772f-108">Ten slotte de sensorgegevens verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2772f-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2772f-109">Als u andere boards ESP8266 gebruikt, kunt u deze stappen om te verbinden met uw IoT-hub nog steeds volgen.</span><span class="sxs-lookup"><span data-stu-id="2772f-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="2772f-110">Afhankelijk van de ESP8266 bestuur u gebruikt, moet u mogelijk opnieuw configureren de `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="2772f-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="2772f-111">Bijvoorbeeld, als u ESP8266 van AI Thinker gebruikt, u kunt wijzigen in `0` naar `2`.</span><span class="sxs-lookup"><span data-stu-id="2772f-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="2772f-112">Een kit nog geen hebt?: klik op [hier](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="2772f-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2772f-113">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2772f-113">What you will learn</span></span>

* <span data-ttu-id="2772f-114">Het maken van een IoT-hub en een apparaat registreren voor voor ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="2772f-115">Hoe ding Dev verbinding met de sensor en uw computer.</span><span class="sxs-lookup"><span data-stu-id="2772f-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="2772f-116">Het verzamelen van sensorgegevens door het uitvoeren van een voorbeeld van toepassing op wat ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="2772f-117">Hoe de sensorgegevens verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2772f-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="2772f-118">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2772f-118">What you will need</span></span>

![Onderdelen die nodig zijn voor de zelfstudie](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="2772f-120">Om deze bewerking niet voltooien, moet u de volgende onderdelen van uw ding Developer Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="2772f-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="2772f-121">De Sparkfun ESP8266 ding Dev-kaart.</span><span class="sxs-lookup"><span data-stu-id="2772f-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="2772f-122">Een Micro USB-Type A USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="2772f-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="2772f-123">Ook moet u het volgende voor uw ontwikkelomgeving:</span><span class="sxs-lookup"><span data-stu-id="2772f-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="2772f-124">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2772f-124">An active Azure subscription.</span></span> <span data-ttu-id="2772f-125">Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="2772f-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2772f-126">Mac of PC met Windows of Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2772f-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="2772f-127">Sparkfun ESP8266 ding Dev verbinding maken met draadloze netwerk.</span><span class="sxs-lookup"><span data-stu-id="2772f-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="2772f-128">Internet-verbinding voor het downloaden van het hulpprogramma voor serverconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="2772f-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="2772f-129">[Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 (of nieuwer), eerdere versies werkt niet met de AzureIoT-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="2772f-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="2772f-130">De volgende items zijn optioneel als u een sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="2772f-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="2772f-131">U hebt ook de optie van het gebruik van gesimuleerde sensorgegevens.</span><span class="sxs-lookup"><span data-stu-id="2772f-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="2772f-132">Een Adafruit DHT22-sensor van temperatuur en vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="2772f-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="2772f-133">Een breadboard.</span><span class="sxs-lookup"><span data-stu-id="2772f-133">A breadboard.</span></span>
* <span data-ttu-id="2772f-134">M/M meestal bedrading.</span><span class="sxs-lookup"><span data-stu-id="2772f-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="2772f-135">ESP8266 ding Dev verbinden met de sensor en uw computer</span><span class="sxs-lookup"><span data-stu-id="2772f-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="2772f-136">Verbinding maken met een DHT22 temperatuur en vochtigheid sensor ESP8266 ding Dev</span><span class="sxs-lookup"><span data-stu-id="2772f-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="2772f-137">Gebruik de bedrading breadboard en meestal als volgt verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="2772f-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="2772f-138">Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2772f-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Verbindingen verwijzing](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="2772f-140">We gebruiken de volgende bedrading voor sensor-pincodes:</span><span class="sxs-lookup"><span data-stu-id="2772f-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="2772f-141">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="2772f-141">Start (Sensor)</span></span>           | <span data-ttu-id="2772f-142">Einde (BMC)</span><span class="sxs-lookup"><span data-stu-id="2772f-142">End (Board)</span></span>           | <span data-ttu-id="2772f-143">Kleur van de kabel</span><span class="sxs-lookup"><span data-stu-id="2772f-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2772f-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="2772f-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="2772f-145">3v (8A pincode)</span><span class="sxs-lookup"><span data-stu-id="2772f-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="2772f-146">Rode-kabel</span><span class="sxs-lookup"><span data-stu-id="2772f-146">Red cable</span></span>     |
| <span data-ttu-id="2772f-147">GEGEVENS (Pin 28 septies)</span><span class="sxs-lookup"><span data-stu-id="2772f-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="2772f-148">GPIO 2 (9A pincode)</span><span class="sxs-lookup"><span data-stu-id="2772f-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="2772f-149">Witte kabel</span><span class="sxs-lookup"><span data-stu-id="2772f-149">White cable</span></span>    |
| <span data-ttu-id="2772f-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="2772f-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="2772f-151">GND (7J pincode)</span><span class="sxs-lookup"><span data-stu-id="2772f-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="2772f-152">Zwarte kabel</span><span class="sxs-lookup"><span data-stu-id="2772f-152">Black cable</span></span>   |


- <span data-ttu-id="2772f-153">Zie voor meer informatie: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) en [Sparkfun ESP8266 ding Dev-specificatie](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="2772f-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="2772f-154">Nu moeten uw Sparkfun ESP8266 ding Dev zijn verbonden met een sensor werken.</span><span class="sxs-lookup"><span data-stu-id="2772f-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![verbinding maken met dht22 met ESP8266 ding Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="2772f-156">Sparkfun ESP8266 ding Dev aansluiten op uw computer</span><span class="sxs-lookup"><span data-stu-id="2772f-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="2772f-157">Gebruik de Micro USB-poort Type A USB-kabel Sparkfun ESP8266 ding Dev op uw computer als volgt verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="2772f-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![Doezelaar huzzah aansluiten op uw computer](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="2772f-159">Machtigingen van de seriële poort – Ubuntu alleen toevoegen</span><span class="sxs-lookup"><span data-stu-id="2772f-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="2772f-160">Als u Ubuntu gebruikt, controleert u of dat een normale gebruiker heeft de machtigingen om te werken op de USB-poort van Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="2772f-161">Als u wilt toevoegen seriële poort machtigingen voor een normale gebruiker, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2772f-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="2772f-162">Voer de volgende opdrachten in een terminal:</span><span class="sxs-lookup"><span data-stu-id="2772f-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="2772f-163">U kunt een van de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="2772f-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="2772f-164">CRW-rw---1 hoofdmap uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="2772f-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="2772f-165">CRW-rw---1 hoofdmap bellen xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="2772f-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="2772f-166">U ziet in de uitvoer van de `uucp` of `dialout` die groepsnaam van de eigenaar van de USB-poort.</span><span class="sxs-lookup"><span data-stu-id="2772f-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="2772f-167">De gebruiker toevoegen aan de groep met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2772f-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="2772f-168">`<group-owner-name>`is de naam van de eigenaar die u in de vorige stap hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="2772f-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="2772f-169">`<username>`uw gebruikersnaam Ubuntu is.</span><span class="sxs-lookup"><span data-stu-id="2772f-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="2772f-170">Ubuntu afmelden en aanmelden voor deze opnieuw om de wijziging door te voeren.</span><span class="sxs-lookup"><span data-stu-id="2772f-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="2772f-171">Sensorgegevens verzamelen en verzenden naar uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="2772f-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="2772f-172">In deze sectie kunt u gegevens kunt implementeren en uitvoeren van een voorbeeldtoepassing op Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="2772f-173">De voorbeeldtoepassing de LED Sparkfun ESP8266 ding Dev knippert en stuurt de temperatuur en vochtigheid gegevens verzameld van de sensor DHT22 naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2772f-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="2772f-174">Ophalen van de voorbeeldtoepassing uit GitHub</span><span class="sxs-lookup"><span data-stu-id="2772f-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="2772f-175">De voorbeeldtoepassing wordt gehost op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2772f-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="2772f-176">Kloon de opslagplaats voorbeeld waarin de voorbeeldtoepassing vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="2772f-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="2772f-177">De voorbeeld-opslagplaats klonen, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2772f-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="2772f-178">Open een opdrachtprompt of een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="2772f-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="2772f-179">Ga naar een map waar u de voorbeeldtoepassing moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2772f-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="2772f-180">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="2772f-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="2772f-181">Installeer het pakket voor Sparkfun ESP8266 ding Dev Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="2772f-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="2772f-182">Open de map waar de voorbeeldtoepassing wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2772f-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="2772f-183">Open het bestand app.ino in de map van de app in Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="2772f-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![de voorbeeldtoepassing in arduino ide openen](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="2772f-185">Klik in de IDE Arduino **bestand** > **voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="2772f-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="2772f-186">In de **voorkeuren** dialoogvenster vak, klik op het pictogram naast de **extra Boards Manager-URL's** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2772f-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="2772f-187">Voer de volgende URL in het pop-upvenster en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2772f-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Wijs de url van een pakket in arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="2772f-189">In de **voorkeur** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2772f-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="2772f-190">Klik op **extra** > **mededelingenbord** > **Boards Manager**, en zoek vervolgens naar esp8266.</span><span class="sxs-lookup"><span data-stu-id="2772f-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="2772f-191">ESP8266 met een versie van 2.2.0 of later moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2772f-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Het pakket esp8266 is geïnstalleerd](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="2772f-193">Klik op **extra** > **mededelingenbord** > **Sparkfun ESP8266 ding Dev**.</span><span class="sxs-lookup"><span data-stu-id="2772f-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="2772f-194">Vereiste bibliotheken installeren</span><span class="sxs-lookup"><span data-stu-id="2772f-194">Install necessary libraries</span></span>

1. <span data-ttu-id="2772f-195">Klik in de IDE Arduino **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.</span><span class="sxs-lookup"><span data-stu-id="2772f-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="2772f-196">Zoeken naar de volgende bibliotheek benoemt één voor één.</span><span class="sxs-lookup"><span data-stu-id="2772f-196">Search for the following library names one by one.</span></span> <span data-ttu-id="2772f-197">Voor elk van de bibliotheek die u wilt zoeken, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="2772f-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="2772f-198">Geen een echte DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="2772f-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="2772f-199">De voorbeeldtoepassing kunt temperatuur en vochtigheid gegevens simuleren als u een echte DHT22 sensor geen hebt.</span><span class="sxs-lookup"><span data-stu-id="2772f-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="2772f-200">Schakel in de voorbeeldtoepassing gesimuleerde gegevens gebruiken door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2772f-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="2772f-201">Open de `config.h` bestand de `app` map.</span><span class="sxs-lookup"><span data-stu-id="2772f-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="2772f-202">Zoek de volgende regel code en wijzig de waarde van `false` naar `true`:</span><span class="sxs-lookup"><span data-stu-id="2772f-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configureren van de voorbeeldtoepassing gesimuleerde gegevens gebruiken](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="2772f-204">Sla met `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="2772f-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="2772f-205">De voorbeeldtoepassing voor Sparkfun ESP8266 ding Dev implementeren</span><span class="sxs-lookup"><span data-stu-id="2772f-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="2772f-206">Klik in de IDE Arduino **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort voor voor Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="2772f-207">Klik op **schema** > **uploaden** kunnen bouwen en implementeren van de voorbeeldtoepassing voor Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="2772f-208">Als u van Mac OS gebruikmaakt kan waarschijnlijk ziet u de volgende berichten tijdens het uploaden.</span><span class="sxs-lookup"><span data-stu-id="2772f-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="2772f-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="2772f-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="2772f-210">Open uw ternimal-venster en klaar bent met het onderstaande bewerkingen u dit probleem kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="2772f-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="2772f-211">Voer uw referenties in</span><span class="sxs-lookup"><span data-stu-id="2772f-211">Enter your credentials</span></span>

<span data-ttu-id="2772f-212">Nadat het uploaden voltooid is, volg u de stappen om uw referenties invoeren:</span><span class="sxs-lookup"><span data-stu-id="2772f-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="2772f-213">Klik in de IDE Arduino **extra** > **seriële Monitor**.</span><span class="sxs-lookup"><span data-stu-id="2772f-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="2772f-214">In het venster seriële monitor ziet u de twee lijsten in de vervolgkeuzelijst in de rechterbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="2772f-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="2772f-215">Selecteer **er is geen afsluitende regel** voor de linker vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2772f-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="2772f-216">Selecteer **115200 baud** voor de lijst rechts vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2772f-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="2772f-217">Voer de volgende gegevens in het invoervak zich boven aan het venster seriële monitor, als u wordt gevraagd om ze en klik vervolgens op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="2772f-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="2772f-218">Wi-Fi-SSID</span><span class="sxs-lookup"><span data-stu-id="2772f-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="2772f-219">Wi-Fi-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="2772f-219">Wi-Fi password</span></span>
   * <span data-ttu-id="2772f-220">Apparaat-verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="2772f-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="2772f-221">De referentie-informatie wordt opgeslagen in de EEPROM van Sparkfun ESP8266 ding ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="2772f-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="2772f-222">Als u op de knop herstellen op het mededelingenbord Sparkfun ESP8266 ding Dev, de voorbeeldtoepassing wordt gevraagd of u wilt de gegevens wissen.</span><span class="sxs-lookup"><span data-stu-id="2772f-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="2772f-223">Voer `Y` om de informatie die wordt gewist en wordt u gevraagd de gegevens opnieuw te verstrekken.</span><span class="sxs-lookup"><span data-stu-id="2772f-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="2772f-224">Controleer of dat de voorbeeldtoepassing met succes wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="2772f-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="2772f-225">Als u de volgende uitvoer van het monitorvenster seriële en de knipperende LED op Sparkfun ESP8266 ding Dev ziet, wordt de voorbeeldtoepassing met succes uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2772f-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![uiteindelijke uitvoer arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="2772f-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2772f-227">Next steps</span></span>

<span data-ttu-id="2772f-228">U hebt een Dev Sparkfun ESP8266 wat is verbonden met uw IoT-hub en de vastgelegde sensorgegevens verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2772f-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
