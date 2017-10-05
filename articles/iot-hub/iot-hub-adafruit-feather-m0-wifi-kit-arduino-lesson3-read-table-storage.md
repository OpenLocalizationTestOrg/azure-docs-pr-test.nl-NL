---
title: 'Connect Arduino (C) naar Azure IoT - les 3: Table storage | Microsoft Docs'
description: De apparaat-naar-cloud-berichten bewaken omdat ze naar uw Azure Table-opslag zijn geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29fb97f5cf0669acb9e68d8a829294ee64c9cf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="1c164-104">Alleen berichten permanent in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1c164-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1c164-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="1c164-105">What you will do</span></span>
<span data-ttu-id="1c164-106">Controleer de apparaat-naar-cloud-berichten die vanaf het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino naar uw IoT-hub worden verzonden omdat de berichten naar uw Azure Table-opslag zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="1c164-106">Monitor the device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board to your IoT hub as the messages are written to your Azure Table storage.</span></span>

<span data-ttu-id="1c164-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1c164-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1c164-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1c164-108">What you will learn</span></span>
<span data-ttu-id="1c164-109">In dit artikel leert u hoe u met de taak bericht lezen gulp lezen berichten permanent in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="1c164-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1c164-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="1c164-110">What you need</span></span>
<span data-ttu-id="1c164-111">Voordat u deze procedure begint, moet is voltooid [de voorbeeldtoepassing Azure knipperen uitvoeren op het mededelingenbord Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="1c164-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="1c164-112">Nieuwe berichten in uw storage-account lezen</span><span class="sxs-lookup"><span data-stu-id="1c164-112">Read new messages from your storage account</span></span>
<span data-ttu-id="1c164-113">In het vorige artikel kunt u een voorbeeld van toepassing op het mededelingenbord Arduino uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1c164-113">In the previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="1c164-114">De voorbeeld-toepassing verzonden berichten naar uw Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="1c164-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="1c164-115">De verzonden naar uw IoT-hub berichten worden opgeslagen in uw Azure Table storage via de Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="1c164-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="1c164-116">U moet de verbindingsreeks voor Azure-opslag om berichten te lezen uit uw Azure-tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="1c164-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="1c164-117">Als u wilt lezen van berichten die zijn opgeslagen in uw Azure Table storage, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="1c164-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="1c164-118">De verbindingsreeks ophalen met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1c164-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="1c164-119">De eerste opdracht haalt de `storage name` die wordt gebruikt in de tweede opdracht om de verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="1c164-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="1c164-120">Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1c164-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="1c164-121">Open het configuratiebestand `config-arduino.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1c164-121">Open the configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="1c164-122">Vervang `[Azure storage connection string]` met de verbindingsreeks die u in stap 1 hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="1c164-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="1c164-123">Sla de `config-arduino.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="1c164-123">Save the `config-arduino.json` file.</span></span>
5. <span data-ttu-id="1c164-124">Berichten opnieuw verzenden en ze uit uw Azure-tabelopslag lezen door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="1c164-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="1c164-125">De logica voor het lezen van Azure Table storage is in de `azure-table.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="1c164-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp uitgevoerd--lezen-opslag][gulp-run]

## <a name="summary"></a><span data-ttu-id="1c164-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="1c164-127">Summary</span></span>
<span data-ttu-id="1c164-128">U hebt is het mededelingenbord Arduino verbonden met uw IoT-hub in de cloud en de voorbeeldtoepassing knipperen gebruikt om apparaat-naar-cloud-berichten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="1c164-128">You've successfully connected your Arduino board to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="1c164-129">U hebt ook de functie Azure-app gebruikt voor het opslaan van IoT hub berichten naar uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="1c164-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="1c164-130">Nu kunt u op het mededelingenbord Arduino cloud-naar-apparaat-berichten uit uw IoT-hub verzenden.</span><span class="sxs-lookup"><span data-stu-id="1c164-130">You can now send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c164-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c164-131">Next steps</span></span>
<span data-ttu-id="1c164-132">[Cloud-naar-apparaat-berichten verzenden][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="1c164-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md