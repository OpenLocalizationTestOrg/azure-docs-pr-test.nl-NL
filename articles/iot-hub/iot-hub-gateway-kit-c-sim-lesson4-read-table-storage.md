---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: Table storage | Microsoft Docs'
description: Intel NUC berichten opslaan op uw IoT-hub, geschreven naar Azure Table storage en ze vervolgens vanuit de cloud te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens ophalen uit de cloud, iot-cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="5d49f-104">Alleen berichten permanent in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="5d49f-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5d49f-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5d49f-105">What you will do</span></span>

- <span data-ttu-id="5d49f-106">De voorbeeldtoepassing gateway uitvoeren op uw gateway dat berichten naar uw IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="5d49f-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="5d49f-107">Voorbeeldcode uitvoeren op de hostcomputer lezen van berichten in uw Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="5d49f-107">Run sample code on your host computer to read messages in your Azure Table storage.</span></span>

<span data-ttu-id="5d49f-108">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5d49f-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5d49f-109">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5d49f-109">What you will learn</span></span>

<span data-ttu-id="5d49f-110">Het gebruik van het hulpprogramma gulp de voorbeeldcode om te lezen van berichten in uw Azure-tabelopslag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5d49f-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5d49f-111">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5d49f-111">What you need</span></span>

<span data-ttu-id="5d49f-112">U hebt met succes uitgevoerd de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="5d49f-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="5d49f-113">[De functie Azure-app en de Azure storage-account gemaakt](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="5d49f-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="5d49f-114">[Uitvoeren van de voorbeeldtoepassing gateway](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d49f-114">[Run the gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="5d49f-115">[Lezen van berichten uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5d49f-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="5d49f-116">Uw Azure storage-verbindingsreeksen ophalen</span><span class="sxs-lookup"><span data-stu-id="5d49f-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="5d49f-117">In deze les vroeg u een Azure storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d49f-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="5d49f-118">Als u de verbindingsreeks van de Azure storage-account, voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5d49f-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="5d49f-119">Lijst van alle opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="5d49f-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="5d49f-120">Azure-opslag-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="5d49f-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="5d49f-121">Gebruik `iot-gateway` als de waarde van `{resource group name}` als u de waarde in les 2 is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5d49f-121">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="5d49f-122">De apparaatverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="5d49f-122">Configure the device connection</span></span>

<span data-ttu-id="5d49f-123">Update de `config-azure.json` bestand zodat de voorbeeldcode die wordt uitgevoerd op de computer in uw Azure-tabelopslag bericht kan lezen.</span><span class="sxs-lookup"><span data-stu-id="5d49f-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="5d49f-124">Volg deze stappen voor het configureren van de apparaatverbinding:</span><span class="sxs-lookup"><span data-stu-id="5d49f-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="5d49f-125">Open het configuratiebestand van het apparaat `config-azure.json` met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5d49f-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuratie](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="5d49f-127">Vervang `[Azure storage connection string]` met de verbindingsreeks voor Azure-opslag die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="5d49f-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="5d49f-128">`[IoT hub connection string]`al in de sectie moet worden vervangen [berichten lezen uit Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span><span class="sxs-lookup"><span data-stu-id="5d49f-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="5d49f-129">Lezen van berichten in uw Azure-tabelopslag</span><span class="sxs-lookup"><span data-stu-id="5d49f-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="5d49f-130">Voer de voorbeeldtoepassing gateway en Azure Table storage berichten gelezen door de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5d49f-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="5d49f-131">Uw IoT-hub wordt geactiveerd voor uw toepassing Azure-functie in het bericht in uw Azure-tabelopslag op te slaan wanneer nieuw bericht binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="5d49f-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="5d49f-132">De `gulp run` opdracht wordt uitgevoerd voor gateway-voorbeeldtoepassing die berichten naar uw IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="5d49f-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="5d49f-133">Met `table-storage` parameter, dit kan een onderliggend proces voor het ontvangen van het bericht opgeslagen in uw Azure-tabelopslag ook gestart.</span><span class="sxs-lookup"><span data-stu-id="5d49f-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="5d49f-134">De berichten die worden verzonden en ontvangen, worden alle weergegeven onmiddellijk op de dezelfde consolevenster in de hostmachine.</span><span class="sxs-lookup"><span data-stu-id="5d49f-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="5d49f-135">Het exemplaar van de steekproef wordt beëindigd automatisch op 40 seconden.</span><span class="sxs-lookup"><span data-stu-id="5d49f-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp lezen](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="5d49f-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5d49f-137">Summary</span></span>

<span data-ttu-id="5d49f-138">U kunt de voorbeeldcode om te lezen van de berichten in uw Azure-tabelopslag opgeslagen door de toepassing van uw Azure-functie hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5d49f-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>
