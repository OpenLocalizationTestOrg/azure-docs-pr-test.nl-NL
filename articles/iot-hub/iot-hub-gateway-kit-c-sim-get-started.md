---
title: Gesimuleerde apparaat & Azure IoT Gateway - aan de slag | Microsoft Docs
description: Aan de slag met IoT Gateway Starter Kit, maakt u uw Azure-IoT-hub en verbinding maken met de Gateway met de iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, iot-gateway aan de slag met het internet der dingen, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="d57ff-104">Aan de slag met IoT Gateway Starter Kit met een gesimuleerd apparaat</span><span class="sxs-lookup"><span data-stu-id="d57ff-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d57ff-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="d57ff-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="d57ff-106">Gesimuleerde apparaat</span><span class="sxs-lookup"><span data-stu-id="d57ff-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="d57ff-107">In deze zelfstudie maakt u eerst leren over het werken met [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="d57ff-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="d57ff-108">U werkt met Intel NUC die o de Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d57ff-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="d57ff-109">U leert hoe seamleesly verbinding maken uw apparaten naar de cloud met behulp van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d57ff-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="d57ff-110">**Een kit nog geen hebt?:** klikt u op [hier](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="d57ff-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="d57ff-111">Les 1: Uw NUC configureren</span><span class="sxs-lookup"><span data-stu-id="d57ff-111">Lesson 1: Configure your NUC</span></span>
![Lesson1 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="d57ff-113">In deze les Intel NUC (volgende eenheid van computers) in de set als een Azure IoT gateway instellen, de rand van Azure IoT-pakket op NUC installeren en uitvoeren van een voorbeeld-app om te controleren of de functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="d57ff-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="d57ff-114">*Geschatte duur: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="d57ff-115">Ga naar [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="d57ff-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="d57ff-116">Les 2: Uw IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="d57ff-116">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="d57ff-118">In deze les installeert u de hulpprogramma's en software op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="d57ff-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="d57ff-119">Vervolgens maken uw gratis Azure-account, het inrichten van uw Azure-IoT-hub en maken van uw eerste apparaat in de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d57ff-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="d57ff-120">Les 1 voltooien voordat u deze les.</span><span class="sxs-lookup"><span data-stu-id="d57ff-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="d57ff-121">Hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="d57ff-121">Get the tools</span></span>
<span data-ttu-id="d57ff-122">De hulpprogramma's en -software installeren op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="d57ff-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="d57ff-123">*Geschatte duur: 20 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="d57ff-124">Ga naar [Download de hulpprogramma's](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="d57ff-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="d57ff-125">Een iothub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="d57ff-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="d57ff-126">Uw eerste apparaat toevoegen aan de iothub met de Azure CLI uw resourcegroep maken en inrichten van uw eerste Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d57ff-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="d57ff-127">*Geschatte duur: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="d57ff-128">Ga naar [een iothub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="d57ff-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="d57ff-129">Les 3: Berichten ontvangen van het gesimuleerde apparaat en de berichten lezen uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="d57ff-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="d57ff-130">In deze les wordt u scripts gebruiken voor het automatiseren van de configuratie en uitvoering van een gesimuleerde apparaattoepassing in uw gateway.</span><span class="sxs-lookup"><span data-stu-id="d57ff-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="d57ff-131">De gesimuleerde apparaattoepassing temperatuur voorbeeldgegevens genereert en verzendt het naar een IoT hub-module.</span><span class="sxs-lookup"><span data-stu-id="d57ff-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="d57ff-132">De module IoT-hub pakketten van de ontvangen gegevens en verzendt het naar uw IoT-hub via het gateway-framework dat is opgegeven in de Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="d57ff-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Les 3 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="d57ff-134">Configureren en uitvoeren van een gesimuleerd apparaat</span><span class="sxs-lookup"><span data-stu-id="d57ff-134">Configure and run a simulated device</span></span>
<span data-ttu-id="d57ff-135">Bereid de voorbeeld-codes.</span><span class="sxs-lookup"><span data-stu-id="d57ff-135">Prepare the sample codes.</span></span> <span data-ttu-id="d57ff-136">Vervolgens configureren en uitvoeren van de voorbeeldtoepassing gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="d57ff-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="d57ff-137">*Geschatte duur: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="d57ff-138">Ga naar [en voer een gesimuleerd apparaat configureren](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="d57ff-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="d57ff-139">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="d57ff-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="d57ff-140">Een voorbeeld van code uitvoeren op de hostcomputer de berichten lezen uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d57ff-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="d57ff-141">*Geschatte duur: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="d57ff-142">Ga naar [berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="d57ff-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="d57ff-143">Les 4: Berichten opslaan in Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="d57ff-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="d57ff-144">Maak een Azure-functie-app die berichten ontvangt van uw IoT-hub en schrijft deze naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="d57ff-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Les 4 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="d57ff-146">Een Azure-functie-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="d57ff-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="d57ff-147">Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure Storage-account te maken.</span><span class="sxs-lookup"><span data-stu-id="d57ff-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="d57ff-148">*Geschatte duur: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="d57ff-149">Ga naar [een Azure-functie-app en Azure Storage-account maken](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="d57ff-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="d57ff-150">Alleen berichten permanent in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="d57ff-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="d57ff-151">De gateway-naar-cloud-berichten bewaken zoals ze zijn geschreven naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="d57ff-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="d57ff-152">*Geschatte duur: 5 minuten*</span><span class="sxs-lookup"><span data-stu-id="d57ff-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="d57ff-153">Ga naar [gelezen berichten permanent in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d57ff-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d57ff-154">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d57ff-154">Troubleshooting</span></span>
<span data-ttu-id="d57ff-155">Als u problemen tijdens de uitkomsten hebt, zoekt u naar oplossingen in de [probleemoplossing](iot-hub-gateway-kit-c-sim-troubleshooting.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d57ff-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="d57ff-156">Meer verkennen</span><span class="sxs-lookup"><span data-stu-id="d57ff-156">Explore more</span></span>
<span data-ttu-id="d57ff-157">Ga naar de [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d57ff-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>