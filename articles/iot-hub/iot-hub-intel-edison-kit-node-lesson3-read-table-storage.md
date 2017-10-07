---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 3: berichten | Microsoft Docs'
description: Hallo apparaat-naar-cloud-berichten bewaken tijdens deze tooyour Azure Table storage worden geschreven.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud hello, cloud gegevensverzameling, iot-cloudservice, iot-gegevens
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="ed8be-104">Alleen berichten permanent in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ed8be-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="ed8be-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="ed8be-105">What you will do</span></span>
<span data-ttu-id="ed8be-106">Monitor Hallo apparaat-naar-cloud-berichten dat uit Intel Edison tooyour iothub worden verzonden als Hallo-berichten worden geschreven tooyour Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="ed8be-106">Monitor hello device-to-cloud messages that are sent from Intel Edison tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="ed8be-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ed8be-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ed8be-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="ed8be-108">What you will learn</span></span>
<span data-ttu-id="ed8be-109">In dit artikel leert u hoe toouse hello gulp bericht lezen taak tooread-berichten permanent in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="ed8be-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ed8be-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="ed8be-110">What you need</span></span>
<span data-ttu-id="ed8be-111">Voordat u deze procedure begint, moet is voltooid [hello Azure knipperen voorbeeldtoepassing uitvoeren op Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="ed8be-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="ed8be-112">Nieuwe berichten in uw storage-account lezen</span><span class="sxs-lookup"><span data-stu-id="ed8be-112">Read new messages from your storage account</span></span>
<span data-ttu-id="ed8be-113">In het vorige artikel hello, kunt u een voorbeeld van toepassing op Edison uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ed8be-113">In hello previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="ed8be-114">Hallo-voorbeeldtoepassing verzonden berichten tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ed8be-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="ed8be-115">IoT-hub tooyour verzonden Hello-berichten worden opgeslagen in uw Azure-tabelopslag via hello Azure functie-app.</span><span class="sxs-lookup"><span data-stu-id="ed8be-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="ed8be-116">U moet Hallo Azure storage connection string tooread berichten uit uw Azure-tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="ed8be-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="ed8be-117">tooread berichten die zijn opgeslagen in uw Azure Table storage, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="ed8be-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="ed8be-118">Hallo-verbindingsreeks ophalen door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="ed8be-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="ed8be-119">de eerste opdracht Hallo haalt Hallo `storage name` die wordt gebruikt in Hallo tweede opdracht tooget Hallo verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="ed8be-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="ed8be-120">Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="ed8be-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="ed8be-121">Open Hallo-configuratiebestand `config-edison.json` in Visual Studio Code door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ed8be-121">Open hello configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="ed8be-122">Vervang `[Azure storage connection string]` met Hallo-verbindingsreeks die u in stap 1 hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="ed8be-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="ed8be-123">Hallo opslaan `config-edison.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="ed8be-123">Save hello `config-edison.json` file.</span></span>
5. <span data-ttu-id="ed8be-124">Berichten opnieuw verzenden en ze door het uitvoeren van de volgende opdracht Hallo uit uw Azure-tabelopslag lezen:</span><span class="sxs-lookup"><span data-stu-id="ed8be-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="ed8be-125">Hallo logica voor het lezen van Azure Table storage is in Hallo `azure-table.js` bestand.</span><span class="sxs-lookup"><span data-stu-id="ed8be-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp uitgevoerd--lezen-opslag][gulp run]

## <a name="summary"></a><span data-ttu-id="ed8be-127">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ed8be-127">Summary</span></span>
<span data-ttu-id="ed8be-128">U hebt met succes Edison tooyour iothub in de cloud Hallo verbonden en hello knipperen voorbeeld toepassing toosend apparaat-naar-cloud-berichten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed8be-128">You've successfully connected Edison tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="ed8be-129">U hebt ook hello Azure functie app toostore binnenkomende IoT hub berichten tooyour Azure Table-opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed8be-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="ed8be-130">Nu kunt u cloud-naar-apparaat-berichten verzenden van uw IoT hub tooEdison.</span><span class="sxs-lookup"><span data-stu-id="ed8be-130">You can now send cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed8be-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed8be-131">Next steps</span></span>
<span data-ttu-id="ed8be-132">[Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="ed8be-132">[Run a sample application tooreceive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md