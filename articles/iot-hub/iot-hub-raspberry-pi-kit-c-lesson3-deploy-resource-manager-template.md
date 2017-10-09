---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 3: implementatie van de sjabloon | Microsoft Docs'
description: Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 11aaad4935681d8b3d338779eec1b19d77cb11e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="e26c6-104">Een Azure-functie-app en Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="e26c6-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="e26c6-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="e26c6-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="e26c6-106">Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="e26c6-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="e26c6-107">Wat doet u</span><span class="sxs-lookup"><span data-stu-id="e26c6-107">What will you do</span></span>
<span data-ttu-id="e26c6-108">Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e26c6-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="e26c6-109">Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.</span><span class="sxs-lookup"><span data-stu-id="e26c6-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="e26c6-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e26c6-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="e26c6-111">Wat leert u</span><span class="sxs-lookup"><span data-stu-id="e26c6-111">What will you learn</span></span>
<span data-ttu-id="e26c6-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="e26c6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="e26c6-113">Hoe toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e26c6-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="e26c6-114">Hoe toouse een Azure app tooprocess IoT hub berichten werken en schrijf deze tooa tabel op Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="e26c6-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="e26c6-115">Wat moet u</span><span class="sxs-lookup"><span data-stu-id="e26c6-115">What do you need</span></span>
* <span data-ttu-id="e26c6-116">U moet hebben voltooid:</span><span class="sxs-lookup"><span data-stu-id="e26c6-116">You must have successfully completed:</span></span>
- [<span data-ttu-id="e26c6-117">Aan de slag met uw frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="e26c6-117">Get started with your Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)
- [<span data-ttu-id="e26c6-118">Uw Azure-IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="e26c6-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="e26c6-119">Open Hallo voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="e26c6-119">Open hello sample app</span></span>
<span data-ttu-id="e26c6-120">Hallo-voorbeeldproject openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="e26c6-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* <span data-ttu-id="e26c6-122">Hallo `main.c` bestand in Hallo `app` submap is Hallo sleutel bronbestand.</span><span class="sxs-lookup"><span data-stu-id="e26c6-122">hello `main.c` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="e26c6-123">Dit bronbestand bevat Hallo code toosend een bericht 20 keer tooyour IoT hub en knipperen Hallo LED voor elk bericht worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="e26c6-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="e26c6-124">Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.</span><span class="sxs-lookup"><span data-stu-id="e26c6-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="e26c6-125">Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e26c6-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="e26c6-126">Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.</span><span class="sxs-lookup"><span data-stu-id="e26c6-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="e26c6-127">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="e26c6-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="e26c6-128">Update Hallo `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e26c6-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager-Sjabloonparameters](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* <span data-ttu-id="e26c6-130">Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd frambozen Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e26c6-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="e26c6-131">Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="e26c6-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="e26c6-132">Hallo voorvoegsel zorgt dat Hallo resourcenaam is globaal unieke tooavoid conflict.</span><span class="sxs-lookup"><span data-stu-id="e26c6-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="e26c6-133">Gebruik geen een streepje of een cijfer initiële in Hallo voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="e26c6-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="e26c6-134">Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="e26c6-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="e26c6-135">Het duurt ongeveer vijf minuten toocreate deze resources.</span><span class="sxs-lookup"><span data-stu-id="e26c6-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="e26c6-136">Tijdens het maken van de resource hello wordt uitgevoerd, kunt u op het volgende artikel toohello.</span><span class="sxs-lookup"><span data-stu-id="e26c6-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="e26c6-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="e26c6-137">Summary</span></span>
<span data-ttu-id="e26c6-138">U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten.</span><span class="sxs-lookup"><span data-stu-id="e26c6-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="e26c6-139">U kunt nu implementeren en uitvoeren van hello voorbeeld toosend apparaat-naar-cloud-berichten met Pi.</span><span class="sxs-lookup"><span data-stu-id="e26c6-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26c6-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e26c6-140">Next steps</span></span>
[<span data-ttu-id="e26c6-141">Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="e26c6-141">Run a sample application toosend device-to-cloud messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

