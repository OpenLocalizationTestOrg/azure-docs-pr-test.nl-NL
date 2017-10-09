---
title: 'Connect Intel Edison (C) tooAzure IoT - les 3: functie-app maken | Microsoft Docs'
description: Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud hello, gegevens die zijn opgeslagen in de cloud, iot cloudservice
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ef045ec2f44fe379a5e6c777d1bfb97de8b965a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2ec25-104">Een Azure-functie-app en Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="2ec25-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="2ec25-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ec25-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="2ec25-106">Een Azure-functie-app fungeert als host Hallo uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec25-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="2ec25-107">Wat doet u</span><span class="sxs-lookup"><span data-stu-id="2ec25-107">What will you do</span></span>
<span data-ttu-id="2ec25-108">Een Azure-functie-app en een Azure storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2ec25-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="2ec25-109">Hello Azure functie-app tooAzure IoT hub gebeurtenissen luistert, binnenkomende berichten worden verwerkt en schrijft deze tooAzure Table storage.</span><span class="sxs-lookup"><span data-stu-id="2ec25-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="2ec25-110">Hallo opslagaccount wordt gebruikt om te lezen Hallo persistent kopieën van berichten vanuit de Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="2ec25-110">hello storage account is used for reading hello persisted copies of messages from Azure table.</span></span> <span data-ttu-id="2ec25-111">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2ec25-111">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="2ec25-112">Wat leert u</span><span class="sxs-lookup"><span data-stu-id="2ec25-112">What will you learn</span></span>
<span data-ttu-id="2ec25-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="2ec25-113">In this article, you will learn:</span></span>
* <span data-ttu-id="2ec25-114">Hoe toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2ec25-114">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="2ec25-115">Hoe toouse een Azure app tooprocess IoT hub berichten werken en schrijf deze tooa tabel op Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="2ec25-115">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="2ec25-116">Wat moet u</span><span class="sxs-lookup"><span data-stu-id="2ec25-116">What do you need</span></span>
<span data-ttu-id="2ec25-117">U moet hebben voltooid:</span><span class="sxs-lookup"><span data-stu-id="2ec25-117">You must have successfully completed:</span></span>
- <span data-ttu-id="2ec25-118">[Aan de slag met uw Edison Intel][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="2ec25-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="2ec25-119">[Uw Azure-IoT-hub maken][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="2ec25-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="2ec25-120">Open Hallo voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="2ec25-120">Open hello sample app</span></span>
<span data-ttu-id="2ec25-121">Hallo-voorbeeldproject openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="2ec25-121">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats][repo-structure]

* <span data-ttu-id="2ec25-123">Hallo-bestand in Hallo `app` submap is Hallo sleutel bronbestand.</span><span class="sxs-lookup"><span data-stu-id="2ec25-123">hello file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="2ec25-124">Dit bronbestand bevat Hallo code toosend een bericht 20 keer tooyour IoT hub en knipperen Hallo LED voor elk bericht worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="2ec25-124">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="2ec25-125">Hallo `arm-template.json` bestand hello Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account is.</span><span class="sxs-lookup"><span data-stu-id="2ec25-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="2ec25-126">Hallo `arm-template-param.json` bestand is Hallo configuratiebestand door hello Azure Resource Manager-sjabloon gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ec25-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="2ec25-127">Hallo `ReceiveDeviceMessages` submap Hallo Node.js-code voor hello Azure functie bevat.</span><span class="sxs-lookup"><span data-stu-id="2ec25-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="2ec25-128">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="2ec25-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="2ec25-129">Update Hallo `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2ec25-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager-Sjabloonparameters][arm-template-parameters]

* <span data-ttu-id="2ec25-131">Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="2ec25-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="2ec25-132">Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="2ec25-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="2ec25-133">Hallo voorvoegsel zorgt dat Hallo resourcenaam is globaal unieke tooavoid conflict.</span><span class="sxs-lookup"><span data-stu-id="2ec25-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="2ec25-134">Gebruik geen een streepje of een cijfer initiële in Hallo voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="2ec25-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="2ec25-135">Na het bijwerken van Hallo `arm-template-param.json` bestand, Hallo resources tooAzure door het uitvoeren van de volgende opdracht Hallo implementeren:</span><span class="sxs-lookup"><span data-stu-id="2ec25-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="2ec25-136">Het duurt ongeveer vijf minuten toocreate deze resources.</span><span class="sxs-lookup"><span data-stu-id="2ec25-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="2ec25-137">Tijdens het maken van de resource hello wordt uitgevoerd, kunt u op het volgende artikel toohello.</span><span class="sxs-lookup"><span data-stu-id="2ec25-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="2ec25-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2ec25-138">Summary</span></span>
<span data-ttu-id="2ec25-139">U uw Azure-functie app-tooprocess IoT hub berichten hebt gemaakt en een Azure-opslag rekening toostore deze berichten.</span><span class="sxs-lookup"><span data-stu-id="2ec25-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="2ec25-140">U kunt nu implementeren en uitvoeren van hello voorbeeld toosend apparaat-naar-cloud-berichten op Edison.</span><span class="sxs-lookup"><span data-stu-id="2ec25-140">You can now deploy and run hello sample toosend device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ec25-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2ec25-141">Next steps</span></span>
<span data-ttu-id="2ec25-142">[Een voorbeeld toepassing toosend apparaat-naar-cloud-berichten worden uitgevoerd op Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="2ec25-142">[Run a sample application toosend device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md