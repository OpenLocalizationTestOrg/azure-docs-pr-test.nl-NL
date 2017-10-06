---
title: 'SensorTag apparaat & Azure IoT Gateway - les 4: Table storage | Microsoft Docs'
description: Berichten uit iothub van Intel NUC tooyour opslaan, tooAzure Table storage geschreven en ze vervolgens vanuit de cloud hello te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens ophalen uit de cloud, iot-cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="f21e1-104">Alleen berichten permanent in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="f21e1-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f21e1-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="f21e1-105">What you will do</span></span>

- <span data-ttu-id="f21e1-106">Hallo gateway voorbeeldtoepassing uitvoeren op uw gateway waarmee berichten tooyour iothub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="f21e1-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="f21e1-107">Voer vervolgens een voorbeeld van code op uw host computer tooread Hallo-berichten in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="f21e1-107">Then run a sample code on your host computer tooread hello messages in your Azure Table storage.</span></span> 

<span data-ttu-id="f21e1-108">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f21e1-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f21e1-109">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="f21e1-109">What you will learn</span></span>

<span data-ttu-id="f21e1-110">Hoe gulp toouse Hallo hulpprogramma toorun Hallo voorbeeld code tooread berichten in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="f21e1-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f21e1-111">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="f21e1-111">What you need</span></span>

<span data-ttu-id="f21e1-112">U hebt met succes Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="f21e1-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="f21e1-113">[Hello Azure functie-app en hello Azure storage-account gemaakt](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="f21e1-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="f21e1-114">[Hallo gateway voorbeeldtoepassing uitvoeren](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="f21e1-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="f21e1-115">[Lezen van berichten uit uw IoT-hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f21e1-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="f21e1-116">Uw Azure storage-verbindingsreeksen ophalen</span><span class="sxs-lookup"><span data-stu-id="f21e1-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="f21e1-117">In deze les vroeg u een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f21e1-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="f21e1-118">Hallo verbindingsreeks tooget van hello Azure storage-account, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f21e1-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="f21e1-119">Lijst van alle opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="f21e1-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="f21e1-120">Azure-opslag-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="f21e1-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="f21e1-121">Iot-gateway gebruiken als de waarde van Hallo `{resource group name}` als u Hallo-waarde in les 2 niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f21e1-121">Use iot-gateway as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="f21e1-122">Hallo apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="f21e1-122">Configure hello device connection</span></span>

<span data-ttu-id="f21e1-123">Update Hallo `config-azure.json` bestand zodat Hallo voorbeeldcode die wordt uitgevoerd op de hostcomputer Hallo bericht in uw Azure Table storage kan lezen.</span><span class="sxs-lookup"><span data-stu-id="f21e1-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="f21e1-124">tooconfigure Hallo apparaatverbinding, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="f21e1-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="f21e1-125">Open Hallo apparaat configuratiebestand `config-azure.json` door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="f21e1-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuratie](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="f21e1-127">Vervang `[Azure storage connection string]` Hello Azure storage-verbindingsreeks die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="f21e1-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="f21e1-128">`[IoT hub connection string]`al in de sectie moet worden vervangen [berichten lezen uit Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span><span class="sxs-lookup"><span data-stu-id="f21e1-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="f21e1-129">Lezen van berichten in uw Azure-tabelopslag</span><span class="sxs-lookup"><span data-stu-id="f21e1-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="f21e1-130">Voer voorbeeldtoepassing Hallo-gateway en Azure Table storage berichten lezen door de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="f21e1-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="f21e1-131">Uw IoT-hub geactiveerd toosave toepassingsbericht van uw Azure-functie in uw Azure-tabelopslag wanneer nieuw bericht binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="f21e1-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="f21e1-132">Hallo `gulp run` opdracht wordt uitgevoerd voor gateway-voorbeeldtoepassing die berichten tooyour iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="f21e1-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="f21e1-133">Met `table-storage` parameter, dit kan een onderliggend proces tooreceive Hallo-bericht opgeslagen in uw Azure-tabelopslag ook gestart.</span><span class="sxs-lookup"><span data-stu-id="f21e1-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="f21e1-134">Hallo-berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op Hallo dezelfde consolevenster in Hallo hostmachine.</span><span class="sxs-lookup"><span data-stu-id="f21e1-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="f21e1-135">Hallo voorbeeld toepassingsexemplaar wordt in 40 seconden automatisch beëindigd.</span><span class="sxs-lookup"><span data-stu-id="f21e1-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp lezen](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="f21e1-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f21e1-137">Summary</span></span>

<span data-ttu-id="f21e1-138">U hebt hello voorbeeld code tooread Hallo-berichten in uw Azure-tabelopslag opgeslagen door de toepassing van uw Azure-functie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f21e1-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
