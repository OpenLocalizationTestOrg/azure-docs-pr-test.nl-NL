---
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een voorbeeldtoepassing in frambozen Pi 3 dat berichten verzendt naar uw IoT-hub en de LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: knipperen cloud pi geleid, knipperen geleid vanuit de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="70e13-104">Voer een voorbeeldtoepassing om apparaat-naar-cloud-berichten te verzenden</span><span class="sxs-lookup"><span data-stu-id="70e13-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="70e13-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="70e13-105">What you will do</span></span>
<span data-ttu-id="70e13-106">In dit artikel wordt beschreven hoe u implementeren en uitvoeren van een voorbeeld van toepassing op frambozen Pi 3 dat berichten naar uw IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="70e13-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="70e13-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="70e13-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="70e13-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="70e13-108">What you will learn</span></span>
<span data-ttu-id="70e13-109">U leert hoe u met het hulpprogramma gulp implementeren en uitvoeren van de voorbeeldtoepassing voor Node.js op Pi.</span><span class="sxs-lookup"><span data-stu-id="70e13-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="70e13-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="70e13-110">What you need</span></span>
* <span data-ttu-id="70e13-111">Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een opslagaccount om te verwerken en opslaan van IoT hub berichten](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="70e13-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="70e13-112">Ophalen van uw IoT-hub en apparaat-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="70e13-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="70e13-113">De verbindingsreeks van het apparaat wordt gebruikt door uw Pi verbinding maken met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="70e13-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="70e13-114">De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinding maken met het identiteitenregister van uw IoT-hub voor het beheren van de apparaten die verbinding maken met uw IoT-hub zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="70e13-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="70e13-115">Een overzicht van uw IoT-hubs in de resourcegroep met de volgende Azure CLI-opdracht:</span><span class="sxs-lookup"><span data-stu-id="70e13-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="70e13-116">Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="70e13-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="70e13-117">De IoT hub-verbindingsreeks ophalen met de volgende opdracht in de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="70e13-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="70e13-118">`{my hub name}`is de naam die u hebt opgegeven als u uw IoT-hub gemaakt en geregistreerd Pi.</span><span class="sxs-lookup"><span data-stu-id="70e13-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="70e13-119">De apparaat-verbindingsreeks ophalen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="70e13-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="70e13-120">Gebruik `myraspberrypi` als de waarde van `{device id}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="70e13-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="70e13-121">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="70e13-121">Configure the device connection</span></span>
1. <span data-ttu-id="70e13-122">Het configuratiebestand initialiseren met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="70e13-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="70e13-123">Open het configuratiebestand van het apparaat `config-raspberrypi.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="70e13-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="70e13-125">Controleer de volgende vervangingen in de `config-raspberrypi.json` bestand:</span><span class="sxs-lookup"><span data-stu-id="70e13-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="70e13-126">Vervang **[apparaat-hostnaam of IP-adres]** met IP-adres of de hostnaam naam van het apparaat u hebt gekregen `device-discovery-cli` of met de waarde die is overgenomen van wanneer u uw apparaat geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="70e13-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="70e13-127">Vervang **[apparaat-verbindingsreeks IoT]** met de `device connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="70e13-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="70e13-128">Vervang **[IoT hub verbindingsreeks]** met de `iot hub connection string` u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="70e13-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="70e13-129">Update de `config-raspberrypi.json` bestand zodat u de voorbeeldtoepassing van uw computer kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="70e13-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="70e13-130">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="70e13-130">Deploy and run the sample application</span></span>
<span data-ttu-id="70e13-131">Implementeren en uitvoeren van de voorbeeldtoepassing op Pi met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="70e13-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="70e13-132">Controleer of de voorbeeldtoepassing werkt</span><span class="sxs-lookup"><span data-stu-id="70e13-132">Verify that the sample application works</span></span>
<span data-ttu-id="70e13-133">U ziet de LED die is verbonden met Pi knippert elke twee seconden.</span><span class="sxs-lookup"><span data-stu-id="70e13-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="70e13-134">Telkens wanneer de LED knippert, wordt de voorbeeldtoepassing verzendt een bericht naar uw IoT-hub en verifieert dat wordt het bericht is verzonden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="70e13-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="70e13-135">Bovendien wordt elk bericht ontvangen door de IoT-hub in het consolevenster.</span><span class="sxs-lookup"><span data-stu-id="70e13-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="70e13-136">De voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="70e13-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="70e13-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="70e13-138">Summary</span></span>
<span data-ttu-id="70e13-139">U hebt geïmplementeerd en de nieuwe knipperen voorbeeldtoepassing uitvoeren op Pi apparaat-naar-cloud-berichten verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="70e13-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="70e13-140">U kunt nu uw berichten bewaken zoals ze zijn geschreven naar het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="70e13-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70e13-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70e13-141">Next steps</span></span>
[<span data-ttu-id="70e13-142">Alleen berichten permanent in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="70e13-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

