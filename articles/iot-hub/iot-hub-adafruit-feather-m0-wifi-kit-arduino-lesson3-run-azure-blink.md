---
title: 'Connect Arduino (C) tooAzure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooAdafruit Doezelaar M0 Wi-Fi dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden gegevens toocloud
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="2ddd7-104">Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="2ddd7-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2ddd7-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="2ddd7-105">What you will do</span></span>
<span data-ttu-id="2ddd7-106">Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op uw Adafruit Doezelaar M0 Wi-Fi Arduino board verzendt berichten tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="2ddd7-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2ddd7-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2ddd7-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="2ddd7-108">What you will learn</span></span>
<span data-ttu-id="2ddd7-109">U leert hoe toouse hello gulp hulpprogramma toodeploy en Hallo Arduino voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2ddd7-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="2ddd7-110">What you need</span></span>
* <span data-ttu-id="2ddd7-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="2ddd7-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="2ddd7-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="2ddd7-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="2ddd7-113">apparaat-verbindingsreeks Hallo gebruikte tooconnect is uw Arduino mededelingenbord tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="2ddd7-114">Hallo IoT hub-verbindingsreeks is gebruikte tooconnect uw IoT hub toohello apparaat-id die uw Arduino vertegenwoordigt board in Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="2ddd7-115">Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="2ddd7-116">Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="2ddd7-117">Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="2ddd7-118">`{my hub name}`Hallo-naam die u hebt opgegeven wanneer u uw IoT-hub gemaakt en het mededelingenbord Arduino geregistreerd is.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="2ddd7-119">Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="2ddd7-120">Gebruik `mym0wifi` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="2ddd7-121">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="2ddd7-121">Configure hello device connection</span></span>
<span data-ttu-id="2ddd7-122">tooconfigure Hallo apparaatverbinding, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="2ddd7-123">Seriële poort Hallo Hallo-apparaat met Hallo apparaat detectie cli verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="2ddd7-124">U moet een uitvoer die vergelijkbaar toohello volgende wordt weergegeven en Hallo usb COM-poort voor het mededelingenbord Arduino vinden:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Detectie van netwerkapparaten][device-discovery]

2. <span data-ttu-id="2ddd7-126">Open Hallo bestand `config.json` in les map Hallo en toe te voegen waarde Hallo Hallo COM-poortnummer gevonden:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="2ddd7-128">Voor Hallo COM-poort op Windows-platform, heeft het Hallo-indeling van `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="2ddd7-129">Op Mac OS of Ubuntu en deze begint met `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="2ddd7-130">Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="2ddd7-131">Open Hallo apparaat configuratiebestand `config-arduino.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config arduino.json][config-arduino-json]

5. <span data-ttu-id="2ddd7-133">Zorg Hallo vervangingen in Hallo na `config-arduino.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="2ddd7-134">Vervang **[Wi-Fi-SSID]** met uw Wi-Fi-SSID die toohello Internet verbonden.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="2ddd7-135">Vervang **[Wi-Fi-wachtwoord]** met het Wi-Fi-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="2ddd7-136">Hallo tekenreeks verwijderen als uw Wi-Fi geen wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="2ddd7-137">Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="2ddd7-138">Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ddd7-139">U hoeft niet `azure_storage_connection_string` in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="2ddd7-140">Houd deze zo is.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2ddd7-141">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="2ddd7-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="2ddd7-142">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op het mededelingenbord Arduino door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ddd7-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="2ddd7-143">Hallo standaard gulp taak wordt uitgevoerd `install-tools` en `run` taken sequentieel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="2ddd7-144">Wanneer u [Hallo knipperen app geïmplementeerd][deployed-the-blink-app], u deze taken afzonderlijk uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="2ddd7-145">Controleer of de voorbeeldtoepassing Hallo werkt</span><span class="sxs-lookup"><span data-stu-id="2ddd7-145">Verify that hello sample application works</span></span>
<span data-ttu-id="2ddd7-146">U ziet Hallo GPIO #0 ingebouwde LED knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="2ddd7-147">Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="2ddd7-148">Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="2ddd7-149">Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="2ddd7-151">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2ddd7-151">Summary</span></span>
<span data-ttu-id="2ddd7-152">U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op uw Arduino mededelingenbord toosend apparaat-naar-cloudberichten tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="2ddd7-153">U nu bewaken uw berichten zoals ze zijn toohello storage-account geschreven.</span><span class="sxs-lookup"><span data-stu-id="2ddd7-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ddd7-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ddd7-154">Next steps</span></span>
<span data-ttu-id="2ddd7-155">[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="2ddd7-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md