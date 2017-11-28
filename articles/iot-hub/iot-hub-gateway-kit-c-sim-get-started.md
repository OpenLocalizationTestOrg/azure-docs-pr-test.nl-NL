---
title: Gesimuleerde apparaat & Azure IoT Gateway - aan de slag | Microsoft Docs
description: Aan de slag met IoT Gateway Starter Kit, maakt u uw Azure-IoT-hub en sluit Gateway toohello iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, iot-gateway aan de slag met Hallo internet der dingen, iot toolkit
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="112e8-104">Aan de slag met IoT Gateway Starter Kit met een gesimuleerd apparaat</span><span class="sxs-lookup"><span data-stu-id="112e8-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="112e8-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="112e8-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="112e8-106">Gesimuleerde apparaat</span><span class="sxs-lookup"><span data-stu-id="112e8-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="112e8-107">In deze zelfstudie maakt u eerst learning Hallo basisbeginselen van het werken met [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="112e8-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="112e8-108">U werkt met Intel NUC die o de Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="112e8-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="112e8-109">U leert hoe tooseamleesly uw apparaten toohello cloud verbinding met behulp van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="112e8-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="112e8-110">**Een kit nog geen hebt?:** klikt u op [hier](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="112e8-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="112e8-111">Les 1: Uw NUC configureren</span><span class="sxs-lookup"><span data-stu-id="112e8-111">Lesson 1: Configure your NUC</span></span>
![Lesson1 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="112e8-113">In deze les Intel NUC (volgende eenheid van computers) instellen in Hallo Kit als een Azure-IoT-gateway, hello Azure IoT rand pakket op NUC installeren en uitvoeren van een voorbeeld-app tooverify Hallo functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="112e8-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="112e8-114">*Geschatte tijd toocomplete: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="112e8-115">Ga te[Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="112e8-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="112e8-116">Les 2: Uw IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="112e8-116">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="112e8-118">In deze les installeert u Hallo-hulpprogramma's en software op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="112e8-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="112e8-119">Vervolgens maken uw gratis Azure-account, het inrichten van uw Azure-IoT-hub en uw eerste apparaat maakt in Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="112e8-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="112e8-120">Les 1 voltooien voordat u deze les.</span><span class="sxs-lookup"><span data-stu-id="112e8-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="112e8-121">Hallo-hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="112e8-121">Get hello tools</span></span>
<span data-ttu-id="112e8-122">Hallo-hulpprogramma's en -software installeren op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="112e8-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="112e8-123">*Geschatte tijd toocomplete: 20 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="112e8-124">Ga te[Hallo-hulpprogramma's ophalen](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="112e8-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="112e8-125">Een iothub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="112e8-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="112e8-126">Toevoegen van uw eerste apparaat toohello IoT-hub hello Azure CLI met uw resourcegroep maken en inrichten van uw eerste Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="112e8-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="112e8-127">*Geschatte tijd toocomplete: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="112e8-128">Ga te[een iothub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="112e8-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="112e8-129">Les 3: Berichten ontvangen van het gesimuleerde apparaat Hallo en berichten lezen uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="112e8-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="112e8-130">In deze les gebruikt u scripts tooautomate Hallo configuratie en uitvoering van een gesimuleerde apparaattoepassing in uw gateway.</span><span class="sxs-lookup"><span data-stu-id="112e8-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="112e8-131">de gesimuleerde apparaattoepassing Hallo temperatuur voorbeeldgegevens genereert en verzendt het tooan IoT hub-module.</span><span class="sxs-lookup"><span data-stu-id="112e8-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="112e8-132">Hallo IoT hub module pakketten Hallo gegevens ontvangen en verzendt deze tooyour IoT-hub door Hallo gateway raamwerk geleverd in Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="112e8-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Les 3 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="112e8-134">Configureren en uitvoeren van een gesimuleerd apparaat</span><span class="sxs-lookup"><span data-stu-id="112e8-134">Configure and run a simulated device</span></span>
<span data-ttu-id="112e8-135">Bereid Hallo voorbeeld codes.</span><span class="sxs-lookup"><span data-stu-id="112e8-135">Prepare hello sample codes.</span></span> <span data-ttu-id="112e8-136">Vervolgens configureren en uitvoeren van de voorbeeldtoepassing voor Hallo gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="112e8-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="112e8-137">*Geschatte tijd toocomplete: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="112e8-138">Ga te[en voer een gesimuleerd apparaat configureren](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="112e8-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="112e8-139">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="112e8-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="112e8-140">Een voorbeeld van code uitvoeren op uw host computer tooread Hallo-berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="112e8-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="112e8-141">*Geschatte tijd toocomplete: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="112e8-142">Ga te[berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="112e8-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="112e8-143">Les 4: Berichten tooAzure Table storage opslaan</span><span class="sxs-lookup"><span data-stu-id="112e8-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="112e8-144">Maak een Azure-functie-app die binnenkomende berichten ontvangt van uw IoT-hub en schrijft deze tooAzure Table storage.</span><span class="sxs-lookup"><span data-stu-id="112e8-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Les 4 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="112e8-146">Een Azure-functie-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="112e8-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="112e8-147">Een Azure-functie-app en een Azure Storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="112e8-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="112e8-148">*Geschatte tijd toocomplete: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="112e8-149">Ga te[een Azure-functie-app en Azure Storage-account maken](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="112e8-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="112e8-150">Alleen berichten permanent in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="112e8-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="112e8-151">Hallo gateway-naar-cloud-berichten bewaken tijdens deze tooAzure Table storage worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="112e8-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="112e8-152">*Geschatte tijd toocomplete: 5 minuten*</span><span class="sxs-lookup"><span data-stu-id="112e8-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="112e8-153">Ga te[gelezen berichten permanent in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="112e8-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="112e8-154">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="112e8-154">Troubleshooting</span></span>
<span data-ttu-id="112e8-155">Als u problemen tijdens Hallo uitkomsten hebt, zoekt u naar oplossingen in Hallo [probleemoplossing](iot-hub-gateway-kit-c-sim-troubleshooting.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="112e8-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="112e8-156">Meer verkennen</span><span class="sxs-lookup"><span data-stu-id="112e8-156">Explore more</span></span>
<span data-ttu-id="112e8-157">Ga naar Hallo [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="112e8-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
