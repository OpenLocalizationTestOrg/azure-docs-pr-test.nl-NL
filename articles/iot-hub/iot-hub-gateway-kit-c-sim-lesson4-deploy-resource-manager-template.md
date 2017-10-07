---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: berichten opslaan | Microsoft Docs'
description: Berichten uit iothub van Intel NUC tooyour opslaan, tooAzure Table storage geschreven en ze vervolgens vanuit de cloud hello te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="588d9-104">Een Azure-functie-app en opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="588d9-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="588d9-105">Azure Functions is een oplossing voor het eenvoudig uitvoeren _functies_ (kleine stukjes code) in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="588d9-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="588d9-106">Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="588d9-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="588d9-107">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="588d9-107">What you will do</span></span>

- <span data-ttu-id="588d9-108">Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="588d9-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="588d9-109">Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.</span><span class="sxs-lookup"><span data-stu-id="588d9-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="588d9-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="588d9-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="588d9-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="588d9-111">What you will learn</span></span>

<span data-ttu-id="588d9-112">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="588d9-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="588d9-113">Hoe toouse Azure Resource Manager toodeploy Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="588d9-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="588d9-114">Hoe toouse een Azure app tooprocess IoT Hub berichten werken en schrijf deze tooa tabel op Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="588d9-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="588d9-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="588d9-115">What you need</span></span>

<span data-ttu-id="588d9-116">U moet hebben voltooid Hallo vorige uitkomsten:</span><span class="sxs-lookup"><span data-stu-id="588d9-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="588d9-117">Les 1: Uw NUC Intel instellen als een IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="588d9-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="588d9-118">Les 2: Bereid u voor uw hostcomputer en Azure IoT hub</span><span class="sxs-lookup"><span data-stu-id="588d9-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="588d9-119">Les 3: Berichten ontvangen van het gesimuleerde apparaat Hallo en berichten lezen uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="588d9-119">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="588d9-120">Een voorbeeld-app openen</span><span class="sxs-lookup"><span data-stu-id="588d9-120">Open a sample app</span></span>

<span data-ttu-id="588d9-121">Ga tooyour `iot-hub-c-intel-nuc-gateway-getting-started` opslagplaats map, initialiseren Hallo-configuratiebestanden en open vervolgens Hallo-voorbeeldproject in Visual Studio Code door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="588d9-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Structuur van de opslagplaats](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="588d9-123">Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.</span><span class="sxs-lookup"><span data-stu-id="588d9-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="588d9-124">Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.</span><span class="sxs-lookup"><span data-stu-id="588d9-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="588d9-125">Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.</span><span class="sxs-lookup"><span data-stu-id="588d9-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="588d9-126">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="588d9-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="588d9-127">Update Hallo `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="588d9-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm-sjabloon json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="588d9-129">Vervang `[your IoT Hub name]` met `{my hub name}` die u hebt opgegeven in les 2.</span><span class="sxs-lookup"><span data-stu-id="588d9-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="588d9-130">Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="588d9-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="588d9-131">Gebruik `iot-gateway` als Hallo-waarde van `{resource group name}` als u Hallo-waarde in les 2 niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="588d9-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="588d9-132">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="588d9-132">Summary</span></span>

<span data-ttu-id="588d9-133">U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten.</span><span class="sxs-lookup"><span data-stu-id="588d9-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="588d9-134">Nu kunt u lezen van berichten die door uw gateway tooyour iothub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="588d9-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="588d9-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="588d9-135">Next steps</span></span>
<span data-ttu-id="588d9-136">[Alleen berichten permanent in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="588d9-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
