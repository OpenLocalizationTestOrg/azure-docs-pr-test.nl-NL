---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 3: Table storage | Microsoft Docs'
description: Hallo apparaat-naar-cloud-berichten bewaken tijdens deze tooyour Azure Table storage worden geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens ophalen uit de cloud, iot-cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 307ce2bc595339790db7379cc011fe262c2b8734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="5945d-104">Alleen berichten permanent in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5945d-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5945d-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5945d-105">What you will do</span></span>
<span data-ttu-id="5945d-106">Monitor Hallo apparaat-naar-cloud-berichten dat uit frambozen Pi 3 tooyour iothub worden verzonden als Hallo-berichten worden geschreven tooyour Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5945d-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="5945d-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5945d-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5945d-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5945d-108">What you will learn</span></span>
<span data-ttu-id="5945d-109">In dit artikel leert u hoe toouse hello gulp bericht lezen taak tooread-berichten permanent in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="5945d-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5945d-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5945d-110">What you need</span></span>
<span data-ttu-id="5945d-111">Voordat u deze procedure begint, moet is voltooid [hello Azure knipperen voorbeeldtoepassing uitvoeren op frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="5945d-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="5945d-112">Nieuwe berichten in uw storage-account lezen</span><span class="sxs-lookup"><span data-stu-id="5945d-112">Read new messages from your storage account</span></span>
<span data-ttu-id="5945d-113">In het vorige artikel hello, kunt u een voorbeeld van toepassing op Pi uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5945d-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="5945d-114">Hallo-voorbeeldtoepassing verzonden berichten tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5945d-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="5945d-115">IoT-hub tooyour verzonden Hello-berichten worden opgeslagen in uw Azure-tabelopslag via hello Azure functie-app.</span><span class="sxs-lookup"><span data-stu-id="5945d-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="5945d-116">U moet Hallo Azure storage connection string tooread berichten uit uw Azure-tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="5945d-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="5945d-117">tooread berichten die zijn opgeslagen in uw Azure Table storage, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5945d-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="5945d-118">Hallo-verbindingsreeks ophalen door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="5945d-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="5945d-119">de eerste opdracht Hallo haalt Hallo `storage name` die wordt gebruikt in Hallo tweede opdracht tooget Hallo verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="5945d-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="5945d-120">Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="5945d-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="5945d-121">Open Hallo-configuratiebestand `config-raspberrypi.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5945d-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="5945d-122">Vervang `[Azure storage connection string]` met Hallo-verbindingsreeks die u in stap 1 hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="5945d-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="5945d-123">Hallo opslaan `config-raspberrypi.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="5945d-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="5945d-124">Berichten opnieuw verzenden en ze door het uitvoeren van de volgende opdracht Hallo uit uw Azure-tabelopslag lezen:</span><span class="sxs-lookup"><span data-stu-id="5945d-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="5945d-125">Hallo logica voor het lezen van Azure Table storage is in Hallo `azure-table.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="5945d-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
   ![gulp uitgevoerd--lezen-opslag](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="5945d-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5945d-127">Summary</span></span>
<span data-ttu-id="5945d-128">U hebt met succes Pi tooyour iothub in de cloud Hallo verbonden en hello knipperen voorbeeld toepassing toosend apparaat-naar-cloud-berichten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5945d-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="5945d-129">U hebt ook hello Azure functie app toostore binnenkomende IoT hub berichten tooyour Azure Table-opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5945d-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="5945d-130">Nu kunt u cloud-naar-apparaat-berichten verzenden van uw IoT hub tooPi.</span><span class="sxs-lookup"><span data-stu-id="5945d-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5945d-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5945d-131">Next steps</span></span>
[<span data-ttu-id="5945d-132">Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="5945d-132">Run a sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

