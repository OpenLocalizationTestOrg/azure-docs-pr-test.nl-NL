---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 4: berichten opslaan | Microsoft Docs'
description: Intel NUC berichten opslaan op uw IoT-hub, geschreven naar Azure Table storage en ze vervolgens vanuit de cloud te lezen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: opslaan van gegevens in de cloud, de gegevens die zijn opgeslagen in de cloud, iot cloudservice
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
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="45b95-104">Een Azure-functie-app en opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="45b95-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="45b95-105">Azure Functions is een oplossing voor het eenvoudig uitvoeren _functies_ (kleine stukjes code) in de cloud.</span><span class="sxs-lookup"><span data-stu-id="45b95-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="45b95-106">Een Azure-functie-app als host fungeert voor de uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="45b95-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="45b95-107">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="45b95-107">What you will do</span></span>

- <span data-ttu-id="45b95-108">Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure storage-account te maken.</span><span class="sxs-lookup"><span data-stu-id="45b95-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="45b95-109">De app Azure functie luistert naar gebeurtenissen van Azure IoT hub, binnenkomende berichten worden verwerkt en schrijft deze naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="45b95-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="45b95-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="45b95-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="45b95-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="45b95-111">What you will learn</span></span>

<span data-ttu-id="45b95-112">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="45b95-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="45b95-113">Het gebruik van Azure Resource Manager voor het implementeren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="45b95-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="45b95-114">Het gebruik van een Azure-functie-app worden IoT Hub berichten verwerken en geschreven naar een tabel in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="45b95-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="45b95-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="45b95-115">What you need</span></span>

<span data-ttu-id="45b95-116">U moet hebt voltooid de vorige uitkomsten:</span><span class="sxs-lookup"><span data-stu-id="45b95-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="45b95-117">Les 1: Uw NUC Intel instellen als een IoT-gateway</span><span class="sxs-lookup"><span data-stu-id="45b95-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="45b95-118">Les 2: Bereid u voor uw hostcomputer en Azure IoT hub</span><span class="sxs-lookup"><span data-stu-id="45b95-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="45b95-119">Les 3: Berichten ontvangen van het gesimuleerde apparaat en de berichten lezen uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="45b95-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="45b95-120">Een voorbeeld-app openen</span><span class="sxs-lookup"><span data-stu-id="45b95-120">Open a sample app</span></span>

<span data-ttu-id="45b95-121">Ga naar uw `iot-hub-c-intel-nuc-gateway-getting-started` opslagplaats map initialiseren van de configuratiebestanden en open vervolgens het voorbeeldproject in Visual Studio Code met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="45b95-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Structuur van de opslagplaats](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="45b95-123">De `arm-template.json` bestand is de Azure Resource Manager-sjabloon met een Azure-functie-app en een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="45b95-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="45b95-124">De `arm-template-param.json` bestand is het configuratiebestand gebruikt door de Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="45b95-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="45b95-125">De `ReceiveDeviceMessages` submap bevat de Node.js-code voor de Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="45b95-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="45b95-126">Configureren van Azure Resource Manager-sjablonen en resources in Azure maken</span><span class="sxs-lookup"><span data-stu-id="45b95-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="45b95-127">Update de `arm-template-param.json` bestand in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="45b95-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm-sjabloon json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="45b95-129">Vervang `[your IoT Hub name]` met `{my hub name}` die u hebt opgegeven in les 2.</span><span class="sxs-lookup"><span data-stu-id="45b95-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="45b95-130">Na het bijwerken van de `arm-template-param.json` bestand, het implementeren van de resources in Azure met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="45b95-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="45b95-131">Gebruik `iot-gateway` als de waarde van `{resource group name}` als u de waarde in les 2 is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="45b95-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="45b95-132">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="45b95-132">Summary</span></span>

<span data-ttu-id="45b95-133">U kunt uw Azure-functie-app voor het verwerken van IoT hub berichten en een Azure storage-account voor het opslaan van deze berichten hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="45b95-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="45b95-134">Nu kunt u lezen van berichten die door uw gateway uit naar uw IoT-hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="45b95-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45b95-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45b95-135">Next steps</span></span>
<span data-ttu-id="45b95-136">[Alleen berichten permanent in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="45b95-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
