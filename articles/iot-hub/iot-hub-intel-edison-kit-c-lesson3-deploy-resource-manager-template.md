---
title: 'Connect Intel Edison (C) naar Azure IoT - les 3: functie-app maken | Microsoft Docs'
description: De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud, de gegevens die zijn opgeslagen in de cloud, iot cloudservice
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
ms.openlocfilehash: 30018cc2d03fc19c13625ef066989a89f21800e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="3f89b-104">Een Azure-functie-app en Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="3f89b-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="3f89b-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud.</span><span class="sxs-lookup"><span data-stu-id="3f89b-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="3f89b-106">Een Azure-functie-app als host fungeert voor de uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f89b-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="3f89b-107">Wat doet u</span><span class="sxs-lookup"><span data-stu-id="3f89b-107">What will you do</span></span>
<span data-ttu-id="3f89b-108">Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure storage-account te maken.</span><span class="sxs-lookup"><span data-stu-id="3f89b-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="3f89b-109">De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="3f89b-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="3f89b-110">Het opslagaccount wordt gebruikt voor het lezen van de persistente kopieën van berichten van het Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="3f89b-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="3f89b-111">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="3f89b-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="3f89b-112">Wat leert u</span><span class="sxs-lookup"><span data-stu-id="3f89b-112">What will you learn</span></span>
<span data-ttu-id="3f89b-113">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="3f89b-113">In this article, you will learn:</span></span>
* <span data-ttu-id="3f89b-114">Het gebruik van [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) voor het implementeren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="3f89b-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="3f89b-115">Het gebruik van een Azure-functie-app voor het verwerken van IoT hub berichten en geschreven naar een tabel in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="3f89b-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="3f89b-116">Wat moet u</span><span class="sxs-lookup"><span data-stu-id="3f89b-116">What do you need</span></span>
<span data-ttu-id="3f89b-117">U moet hebben voltooid:</span><span class="sxs-lookup"><span data-stu-id="3f89b-117">You must have successfully completed:</span></span>
- <span data-ttu-id="3f89b-118">[Aan de slag met uw Edison Intel][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="3f89b-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="3f89b-119">[Uw Azure-IoT-hub maken][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="3f89b-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="3f89b-120">Open de voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="3f89b-120">Open the sample app</span></span>
<span data-ttu-id="3f89b-121">Het voorbeeldproject openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3f89b-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats][repo-structure]

* <span data-ttu-id="3f89b-123">Het bestand in de `app` submap is het belangrijkste bronbestand.</span><span class="sxs-lookup"><span data-stu-id="3f89b-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="3f89b-124">Dit bestand bevat de code voor een bericht 20 keer verzendt naar uw IoT-hub en knipperen de LED voor elk bericht die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3f89b-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="3f89b-125">De `arm-template.json` bestand is de Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="3f89b-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="3f89b-126">De `arm-template-param.json` bestand is het configuratiebestand gebruikt door de Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3f89b-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="3f89b-127">De `ReceiveDeviceMessages` submap bevat de Node.js-code voor de Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="3f89b-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="3f89b-128">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="3f89b-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="3f89b-129">Update de `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3f89b-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager-Sjabloonparameters][arm-template-parameters]

* <span data-ttu-id="3f89b-131">Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="3f89b-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="3f89b-132">Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="3f89b-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="3f89b-133">Het voorvoegsel zorgt ervoor dat de resourcenaam globaal unieke om conflicten te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="3f89b-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="3f89b-134">Gebruik geen een streepje of een cijfer eerste in het voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="3f89b-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="3f89b-135">Na het bijwerken van de `arm-template-param.json` bestand, het implementeren van de resources in Azure met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3f89b-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="3f89b-136">Het duurt ongeveer vijf minuten voor het maken van deze resources.</span><span class="sxs-lookup"><span data-stu-id="3f89b-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="3f89b-137">Tijdens het maken van de resource uitgevoerd wordt, kunt u op het volgende artikel.</span><span class="sxs-lookup"><span data-stu-id="3f89b-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="3f89b-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="3f89b-138">Summary</span></span>
<span data-ttu-id="3f89b-139">U kunt uw Azure-functie-app voor het verwerken van IoT hub berichten en een Azure storage-account voor het opslaan van deze berichten hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f89b-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="3f89b-140">U kunt nu implementeren en uitvoeren van het voorbeeld voor het verzenden van apparaat-naar-cloud-berichten op Edison.</span><span class="sxs-lookup"><span data-stu-id="3f89b-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f89b-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f89b-141">Next steps</span></span>
<span data-ttu-id="3f89b-142">[Voer een voorbeeldtoepassing met apparaat-naar-cloud-berichten verzenden op Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="3f89b-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md