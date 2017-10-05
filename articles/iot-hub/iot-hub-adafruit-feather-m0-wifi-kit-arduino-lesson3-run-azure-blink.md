---
title: 'Connect Arduino (C) naar Azure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een voorbeeldtoepassing met Adafruit Doezelaar M0 Wi-Fi dat berichten verzendt naar uw IoT-hub en de LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden van gegevens naar de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="a3205-104">Voer een voorbeeldtoepassing om apparaat-naar-cloud-berichten te verzenden</span><span class="sxs-lookup"><span data-stu-id="a3205-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a3205-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a3205-105">What you will do</span></span>
<span data-ttu-id="a3205-106">In dit artikel wordt beschreven hoe u implementeren en uitvoeren van een voorbeeld van toepassing op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino dat berichten naar uw IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="a3205-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="a3205-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a3205-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a3205-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a3205-108">What you will learn</span></span>
<span data-ttu-id="a3205-109">U leert hoe u met het hulpprogramma gulp implementeren en uitvoeren van de voorbeeldtoepassing Arduino op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="a3205-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a3205-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a3205-110">What you need</span></span>
* <span data-ttu-id="a3205-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een opslagaccount om te verwerken en opslaan van IoT hub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="a3205-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="a3205-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="a3205-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="a3205-113">De verbindingsreeks van het apparaat wordt gebruikt voor het mededelingenbord Arduino verbinding met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a3205-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="a3205-114">De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinden van uw IoT-hub met de identiteit van het apparaat dat het mededelingenbord Arduino in de IoT-hub vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="a3205-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="a3205-115">Een overzicht van uw IoT-hubs in de resourcegroep met de volgende Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3205-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="a3205-116">Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a3205-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="a3205-117">De IoT hub-verbindingsreeks ophalen met de volgende opdracht in de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="a3205-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="a3205-118">`{my hub name}`is de naam die u hebt opgegeven wanneer u uw IoT-hub gemaakt en het mededelingenbord Arduino geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="a3205-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="a3205-119">De apparaat-verbindingsreeks ophalen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3205-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="a3205-120">Gebruik `mym0wifi` als de waarde van `{device id}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a3205-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="a3205-121">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="a3205-121">Configure the device connection</span></span>
<span data-ttu-id="a3205-122">Volg deze stappen voor het configureren van de apparaatverbinding:</span><span class="sxs-lookup"><span data-stu-id="a3205-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="a3205-123">De seriële poort van het apparaat met de apparaat-detectie cli verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="a3205-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="a3205-124">U moet een uitvoer die vergelijkbaar is met het volgende weergegeven en de usb COM-poort voor het mededelingenbord Arduino vinden:</span><span class="sxs-lookup"><span data-stu-id="a3205-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Detectie van netwerkapparaten][device-discovery]

2. <span data-ttu-id="a3205-126">Open het bestand `config.json` in de map les en voeg de waarde van de COM-poortnummer gevonden:</span><span class="sxs-lookup"><span data-stu-id="a3205-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="a3205-128">Voor de COM-poort op Windows-platform, heeft de indeling van `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="a3205-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="a3205-129">Op Mac OS of Ubuntu en deze begint met `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="a3205-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="a3205-130">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a3205-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="a3205-131">Open het configuratiebestand van het apparaat `config-arduino.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3205-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config arduino.json][config-arduino-json]

5. <span data-ttu-id="a3205-133">Controleer de volgende vervangingen in de `config-arduino.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="a3205-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="a3205-134">Vervang **[Wi-Fi-SSID]** met uw Wi-Fi-SSID die is verbonden met Internet.</span><span class="sxs-lookup"><span data-stu-id="a3205-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="a3205-135">Vervang **[Wi-Fi-wachtwoord]** met het Wi-Fi-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a3205-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="a3205-136">Verwijder de tekenreeks als uw Wi-Fi geen wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="a3205-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="a3205-137">Vervang **[apparaat-verbindingsreeks IoT]** met de `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="a3205-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="a3205-138">Vervang **[IoT hub verbindingsreeks]** met de `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="a3205-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a3205-139">U hoeft niet `azure_storage_connection_string` in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a3205-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="a3205-140">Houd deze zo is.</span><span class="sxs-lookup"><span data-stu-id="a3205-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="a3205-141">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="a3205-141">Deploy and run the sample application</span></span>
<span data-ttu-id="a3205-142">Implementeren en uitvoeren van de voorbeeldtoepassing op het mededelingenbord Arduino met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3205-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="a3205-143">De standaard gulp taak wordt uitgevoerd `install-tools` en `run` taken sequentieel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a3205-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="a3205-144">Wanneer u [de knipperen app hebt geïmplementeerd][deployed-the-blink-app], u deze taken afzonderlijk uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a3205-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="a3205-145">Controleer of de voorbeeldtoepassing werkt</span><span class="sxs-lookup"><span data-stu-id="a3205-145">Verify that the sample application works</span></span>
<span data-ttu-id="a3205-146">U ziet de GPIO #0 ingebouwde LED knippert die per twee seconden.</span><span class="sxs-lookup"><span data-stu-id="a3205-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="a3205-147">Telkens wanneer de LED knippert, wordt de voorbeeldtoepassing verzendt een bericht naar uw IoT-hub en verifieert dat wordt het bericht is verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a3205-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="a3205-148">Bovendien wordt elk bericht ontvangen door de IoT-hub in het consolevenster.</span><span class="sxs-lookup"><span data-stu-id="a3205-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="a3205-149">De voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="a3205-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="a3205-151">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a3205-151">Summary</span></span>
<span data-ttu-id="a3205-152">U hebt geïmplementeerd en de nieuwe knipperen voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino apparaat-naar-cloud-berichten verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a3205-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="a3205-153">U nu bewaken uw berichten zoals ze zijn geschreven naar het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a3205-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3205-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3205-154">Next steps</span></span>
<span data-ttu-id="a3205-155">[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="a3205-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md