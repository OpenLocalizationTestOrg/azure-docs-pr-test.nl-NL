---
featureFlags: usabilla
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 3: Table storage | Microsoft Docs'
description: De apparaat-naar-cloud-berichten bewaken omdat ze naar uw Azure Table-opslag zijn geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gegevens ophalen uit de cloud, iot-cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 60084906c05ff9e5396f8e2378d73f7ac939d8df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="a0fa0-104">Alleen berichten permanent in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a0fa0-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a0fa0-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a0fa0-105">What you will do</span></span>
<span data-ttu-id="a0fa0-106">Controleer de apparaat-naar-cloud-berichten die vanaf frambozen Pi 3 naar uw IoT-hub worden verzonden omdat de berichten naar uw Azure Table-opslag zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="a0fa0-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a0fa0-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0fa0-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a0fa0-108">What you will learn</span></span>
<span data-ttu-id="a0fa0-109">In dit artikel leert u hoe u met de taak bericht lezen gulp lezen berichten permanent in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0fa0-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a0fa0-110">What you need</span></span>
<span data-ttu-id="a0fa0-111">Voordat u deze procedure begint, moet is voltooid [uitvoeren van de voorbeeldtoepassing Azure knipperen op frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="a0fa0-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="a0fa0-112">Nieuwe berichten in uw storage-account lezen</span><span class="sxs-lookup"><span data-stu-id="a0fa0-112">Read new messages from your storage account</span></span>
<span data-ttu-id="a0fa0-113">In het vorige artikel kunt u een voorbeeld van toepassing op Pi uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="a0fa0-114">De voorbeeld-toepassing verzonden berichten naar uw Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="a0fa0-115">De verzonden naar uw IoT-hub berichten worden opgeslagen in uw Azure Table storage via de Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="a0fa0-116">U moet de verbindingsreeks voor Azure-opslag om berichten te lezen uit uw Azure-tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="a0fa0-117">Als u wilt lezen van berichten die zijn opgeslagen in uw Azure Table storage, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a0fa0-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="a0fa0-118">De verbindingsreeks ophalen met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a0fa0-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="a0fa0-119">De eerste opdracht haalt de `storage name` die wordt gebruikt in de tweede opdracht om de verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="a0fa0-120">Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="a0fa0-121">Open het configuratiebestand `config-raspberrypi.json` in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a0fa0-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="a0fa0-122">Vervang `[Azure storage connection string]` met de verbindingsreeks die u in stap 1 hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="a0fa0-123">Sla de `config-raspberrypi.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="a0fa0-124">Berichten opnieuw verzenden en ze uit uw Azure-tabelopslag lezen door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a0fa0-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="a0fa0-125">De logica voor het lezen van Azure Table storage is in de `azure-table.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
    ![gulp uitgevoerd--lezen-opslag](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="a0fa0-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="a0fa0-127">Summary</span></span>
<span data-ttu-id="a0fa0-128">U hebt met succes Pi verbonden met uw IoT-hub in de cloud en de voorbeeldtoepassing knipperen gebruikt om apparaat-naar-cloud-berichten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="a0fa0-129">U hebt ook de functie Azure-app gebruikt voor het opslaan van IoT hub berichten naar uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="a0fa0-130">Nu kunt u cloud-naar-apparaat-berichten verzenden van uw IoT-hub tot Pi.</span><span class="sxs-lookup"><span data-stu-id="a0fa0-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0fa0-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0fa0-131">Next steps</span></span>
[<span data-ttu-id="a0fa0-132">Uitvoeren van de voorbeeldtoepassing cloud-naar-apparaat-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="a0fa0-132">Run the sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

