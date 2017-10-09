---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 3: implementatie van de sjabloon | Microsoft Docs'
description: Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="5eef5-104">Een Azure-functie-app en Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="5eef5-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="5eef5-105">[Azure Functions](../azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="5eef5-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="5eef5-106">Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="5eef5-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5eef5-107">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5eef5-107">What you will do</span></span>
<span data-ttu-id="5eef5-108">Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5eef5-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="5eef5-109">Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5eef5-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="5eef5-110">Als u problemen hebt, zoeken naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5eef5-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5eef5-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5eef5-111">What you will learn</span></span>
<span data-ttu-id="5eef5-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="5eef5-112">In this article, you will learn:</span></span>

* <span data-ttu-id="5eef5-113">Hoe toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span><span class="sxs-lookup"><span data-stu-id="5eef5-113">How toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="5eef5-114">Hoe toouse een Azure app tooprocess IoT hub berichten werken en schrijf deze tooa tabel op Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5eef5-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5eef5-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5eef5-115">What you need</span></span>
<span data-ttu-id="5eef5-116">U moet hebben voltooid:</span><span class="sxs-lookup"><span data-stu-id="5eef5-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="5eef5-117">Aan de slag met frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="5eef5-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="5eef5-118">Uw Azure-IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="5eef5-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="5eef5-119">Open Hallo voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="5eef5-119">Open hello sample app</span></span>
<span data-ttu-id="5eef5-120">Hallo-voorbeeldproject openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="5eef5-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="5eef5-122">Hallo `app.js` bestand in Hallo `app` submap is Hallo sleutel bronbestand.</span><span class="sxs-lookup"><span data-stu-id="5eef5-122">hello `app.js` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="5eef5-123">Dit bronbestand bevat Hallo code toosend een bericht 20 keer tooyour IoT hub en knipperen Hallo LED voor elk bericht worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="5eef5-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="5eef5-124">Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.</span><span class="sxs-lookup"><span data-stu-id="5eef5-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="5eef5-125">Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5eef5-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="5eef5-126">Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.</span><span class="sxs-lookup"><span data-stu-id="5eef5-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="5eef5-127">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="5eef5-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="5eef5-128">Update Hallo `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5eef5-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager-Sjabloonparameters](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="5eef5-130">Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5eef5-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="5eef5-131">Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="5eef5-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="5eef5-132">Hallo voorvoegsel zorgt dat Hallo resourcenaam is globaal unieke tooavoid conflict.</span><span class="sxs-lookup"><span data-stu-id="5eef5-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="5eef5-133">Gebruik geen een streepje of een cijfer initiële in Hallo voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="5eef5-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="5eef5-134">Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="5eef5-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="5eef5-135">Het duurt ongeveer vijf minuten toocreate deze resources.</span><span class="sxs-lookup"><span data-stu-id="5eef5-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="5eef5-136">Tijdens het maken van de resource hello wordt uitgevoerd, kunt u op het volgende artikel toohello.</span><span class="sxs-lookup"><span data-stu-id="5eef5-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="5eef5-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5eef5-137">Summary</span></span>
<span data-ttu-id="5eef5-138">U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten.</span><span class="sxs-lookup"><span data-stu-id="5eef5-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="5eef5-139">U kunt nu implementeren en uitvoeren van hello voorbeeld toosend apparaat-naar-cloud-berichten met Pi.</span><span class="sxs-lookup"><span data-stu-id="5eef5-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eef5-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5eef5-140">Next steps</span></span>
[<span data-ttu-id="5eef5-141">Een voorbeeld toepassing toosend apparaat-naar-cloud-berichten worden uitgevoerd op frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="5eef5-141">Run a sample application toosend device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

