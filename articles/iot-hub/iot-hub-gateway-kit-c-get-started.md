---
title: SensorTag apparaat & Azure IoT Gateway - aan de slag | Microsoft Docs
description: Aan de slag met IoT Gateway Starter Kit, maakt u uw Azure-IoT-hub en verbinding maken met SensorTag en Gateway naar de IoT-hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, iot-gateway aan de slag met het internet der dingen, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="356d3-104">Aan de slag met IoT Gateway Starter Kit met een SensorTag</span><span class="sxs-lookup"><span data-stu-id="356d3-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="356d3-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="356d3-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="356d3-106">Gesimuleerde apparaat</span><span class="sxs-lookup"><span data-stu-id="356d3-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="356d3-107">In deze zelfstudie maakt u eerst leren over het werken met [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="356d3-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="356d3-108">U werkt met Intel NUC die o de Linux wordt uitgevoerd en de [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="356d3-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="356d3-109">U leert hoe seamleesly verbinding maken uw apparaten naar de cloud met behulp van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="356d3-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="356d3-110">**Een kit nog geen hebt?:** klikt u op [hier](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="356d3-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="356d3-111">**Geen een SensorTag?:** [beginnen met een gesimuleerd apparaat](iot-hub-gateway-kit-c-sim-get-started.md) of [een SensorTag kopen](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="356d3-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="356d3-112">Les 1: Uw NUC configureren</span><span class="sxs-lookup"><span data-stu-id="356d3-112">Lesson 1: Configure your NUC</span></span>
![Lesson1 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="356d3-114">In deze les Intel NUC (volgende eenheid van computers) in de set als een Azure IoT gateway instellen, de rand van Azure IoT-pakket op NUC installeren en uitvoeren van een voorbeeld-app om te controleren of de functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="356d3-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="356d3-115">*Geschatte duur: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="356d3-116">Ga naar [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="356d3-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="356d3-117">Les 2: Uw IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="356d3-117">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="356d3-119">In deze les installeert u de hulpprogramma's en software op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="356d3-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="356d3-120">Vervolgens maken uw gratis Azure-account, het inrichten van uw Azure-IoT-hub en maken van uw eerste apparaat in de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="356d3-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="356d3-121">Les 1 voltooien voordat u deze les.</span><span class="sxs-lookup"><span data-stu-id="356d3-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="356d3-122">Hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="356d3-122">Get the tools</span></span>
<span data-ttu-id="356d3-123">De hulpprogramma's en -software installeren op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="356d3-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="356d3-124">*Geschatte duur: 20 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="356d3-125">Ga naar [Download de hulpprogramma's](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="356d3-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="356d3-126">Een iothub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="356d3-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="356d3-127">Uw eerste apparaat toevoegen aan de iothub met de Azure CLI uw resourcegroep maken en inrichten van uw eerste Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="356d3-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="356d3-128">*Geschatte duur: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="356d3-129">Ga naar [een iothub maken en uw apparaat registreren](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="356d3-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="356d3-130">Les 3: Berichten ontvangen van SensorTag en berichten lezen uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="356d3-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="356d3-131">In deze les wordt u scripts gebruiken voor het automatiseren van de configuratie en uitvoering van een voorbeeldtoepassing uitschakelen in uw gateway.</span><span class="sxs-lookup"><span data-stu-id="356d3-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="356d3-132">Dergelijke toepassingen gebruikt u een verzameling van modules voor de statistische functie en transformatie van gegevens, verwerken van opdrachten of een willekeurig aantal gerelateerde taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="356d3-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="356d3-133">Modules communiceren met elkaar via een broker bericht.</span><span class="sxs-lookup"><span data-stu-id="356d3-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="356d3-134">De voorbeeldtoepassing heeft een module uitschakelen en een IoT hub-module.</span><span class="sxs-lookup"><span data-stu-id="356d3-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="356d3-135">De module uitschakelen ontvangt gegevens van SensorTag uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="356d3-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="356d3-136">De module IoT-hub pakketten van de ontvangen gegevens en verzendt het naar uw IoT-hub via het gateway-framework dat is opgegeven in de Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="356d3-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Les 3 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="356d3-138">Configureren en uitvoeren van de voorbeeld-app uitschakelen</span><span class="sxs-lookup"><span data-stu-id="356d3-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="356d3-139">De verbinding tussen de SensorTag en uw gateway instellen.</span><span class="sxs-lookup"><span data-stu-id="356d3-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="356d3-140">Vervolgens de configuratie te voltooien en voer de voorbeeldtoepassing uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="356d3-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="356d3-141">*Geschatte duur: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="356d3-142">Ga naar [configureren en voer de voorbeeld-app uitschakelen](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="356d3-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="356d3-143">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="356d3-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="356d3-144">Voorbeeldcode uitvoeren op de hostcomputer om berichten te lezen uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="356d3-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="356d3-145">*Geschatte duur: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="356d3-146">Ga naar [berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="356d3-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="356d3-147">Les 4: Berichten opslaan in Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="356d3-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="356d3-148">Maak een Azure-functie-app die berichten ontvangt van uw IoT-hub en schrijft deze naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="356d3-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Les 4 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="356d3-150">Een Azure-functie-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="356d3-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="356d3-151">Een Azure Resource Manager-sjabloon gebruiken om een Azure-functie-app en een Azure Storage-account te maken.</span><span class="sxs-lookup"><span data-stu-id="356d3-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="356d3-152">*Geschatte duur: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="356d3-153">Ga naar [een Azure-functie-app en Azure Storage-account maken](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="356d3-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="356d3-154">Alleen berichten permanent in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="356d3-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="356d3-155">De gateway-naar-cloud-berichten bewaken zoals ze zijn geschreven naar Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="356d3-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="356d3-156">*Geschatte duur: 5 minuten*</span><span class="sxs-lookup"><span data-stu-id="356d3-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="356d3-157">Ga naar [gelezen berichten permanent in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="356d3-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="356d3-158">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="356d3-158">Troubleshooting</span></span>
<span data-ttu-id="356d3-159">Als u problemen tijdens de uitkomsten hebt, zoekt u naar oplossingen in de [probleemoplossing](iot-hub-gateway-kit-c-troubleshooting.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="356d3-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="356d3-160">Meer verkennen</span><span class="sxs-lookup"><span data-stu-id="356d3-160">Explore more</span></span>
<span data-ttu-id="356d3-161">Ga naar de [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="356d3-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>