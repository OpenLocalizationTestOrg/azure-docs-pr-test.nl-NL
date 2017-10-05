---
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 3: implementatie van de sjabloon | Microsoft Docs'
description: De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: opslaan van gegevens in de cloud, de gegevens die zijn opgeslagen in de cloud, iot cloudservice
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
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="9960b-104">Een Azure-functie-app en Azure storage-account maken</span><span class="sxs-lookup"><span data-stu-id="9960b-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="9960b-105">[Azure Functions](../azure-functions/functions-overview.md) is een oplossing voor het eenvoudig uitvoeren *functies* (kleine stukjes code) in de cloud.</span><span class="sxs-lookup"><span data-stu-id="9960b-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="9960b-106">Een Azure-functie-app als host fungeert voor de uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="9960b-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9960b-107">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="9960b-107">What you will do</span></span>
<span data-ttu-id="9960b-108">Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure storage-account te maken.</span><span class="sxs-lookup"><span data-stu-id="9960b-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="9960b-109">De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="9960b-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="9960b-110">Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9960b-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9960b-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="9960b-111">What you will learn</span></span>
<span data-ttu-id="9960b-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="9960b-112">In this article, you will learn:</span></span>

* <span data-ttu-id="9960b-113">Het gebruik van [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor het implementeren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="9960b-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="9960b-114">Het gebruik van een Azure-functie-app voor het verwerken van IoT hub berichten en geschreven naar een tabel in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="9960b-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9960b-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="9960b-115">What you need</span></span>
<span data-ttu-id="9960b-116">U moet hebben voltooid:</span><span class="sxs-lookup"><span data-stu-id="9960b-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="9960b-117">Aan de slag met frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="9960b-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="9960b-118">Uw Azure-IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="9960b-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="9960b-119">Open de voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="9960b-119">Open the sample app</span></span>
<span data-ttu-id="9960b-120">Het voorbeeldproject openen in Visual Studio Code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9960b-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Structuur van de opslagplaats](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="9960b-122">De `app.js` bestand de `app` submap is het belangrijkste bronbestand.</span><span class="sxs-lookup"><span data-stu-id="9960b-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="9960b-123">Dit bestand bevat de code voor een bericht 20 keer verzendt naar uw IoT-hub en knipperen de LED voor elk bericht die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9960b-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="9960b-124">De `arm-template.json` bestand is de Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="9960b-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="9960b-125">De `arm-template-param.json` bestand is het configuratiebestand gebruikt door de Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9960b-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="9960b-126">De `ReceiveDeviceMessages` submap bevat de Node.js-code voor de Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="9960b-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="9960b-127">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="9960b-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="9960b-128">Update de `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9960b-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager-Sjabloonparameters](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="9960b-130">Vervang **[naam van uw IoT-Hub]** met **{mijn hubnaam}** die u hebt opgegeven wanneer u [uw IoT-hub gemaakt en geregistreerd frambozen Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9960b-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="9960b-131">Vervang **[voorvoegsel tekenreeks naar nieuwe bronnen]** met een voorvoegsel dat u wilt.</span><span class="sxs-lookup"><span data-stu-id="9960b-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="9960b-132">Het voorvoegsel zorgt ervoor dat de resourcenaam globaal unieke om conflicten te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="9960b-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="9960b-133">Gebruik geen een streepje of een cijfer eerste in het voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="9960b-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="9960b-134">Na het bijwerken van de `arm-template-param.json` bestand, het implementeren van de resources in Azure met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9960b-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="9960b-135">Het duurt ongeveer vijf minuten voor het maken van deze resources.</span><span class="sxs-lookup"><span data-stu-id="9960b-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="9960b-136">Tijdens het maken van de resource uitgevoerd wordt, kunt u op het volgende artikel.</span><span class="sxs-lookup"><span data-stu-id="9960b-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="9960b-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="9960b-137">Summary</span></span>
<span data-ttu-id="9960b-138">U kunt uw Azure-functie-app voor het verwerken van IoT hub berichten en een Azure storage-account voor het opslaan van deze berichten hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9960b-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="9960b-139">U kunt nu implementeren en uitvoeren van het voorbeeld voor het verzenden van apparaat-naar-cloud-berichten met Pi.</span><span class="sxs-lookup"><span data-stu-id="9960b-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9960b-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9960b-140">Next steps</span></span>
[<span data-ttu-id="9960b-141">Voer een voorbeeldtoepassing met apparaat-naar-cloud-berichten verzenden op frambozen Pi 3</span><span class="sxs-lookup"><span data-stu-id="9960b-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

