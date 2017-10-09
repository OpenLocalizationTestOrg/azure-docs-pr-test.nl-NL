---
title: SensorTag apparaat & Azure IoT Gateway - aan de slag | Microsoft Docs
description: Aan de slag met IoT Gateway Starter Kit, maakt u uw Azure-IoT-hub en sluit SensorTag en Gateway toohello iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, iot-gateway aan de slag met Hallo internet der dingen, iot toolkit
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
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="1f33c-104">Aan de slag met IoT Gateway Starter Kit met een SensorTag</span><span class="sxs-lookup"><span data-stu-id="1f33c-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f33c-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="1f33c-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="1f33c-106">Gesimuleerde apparaat</span><span class="sxs-lookup"><span data-stu-id="1f33c-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="1f33c-107">In deze zelfstudie maakt u eerst learning Hallo basisbeginselen van het werken met [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="1f33c-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="1f33c-108">U werkt met Intel NUC met o de Linux- en Hallo [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="1f33c-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="1f33c-109">U leert hoe tooseamleesly uw apparaten toohello cloud verbinding met behulp van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1f33c-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="1f33c-110">**Een kit nog geen hebt?:** klikt u op [hier](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="1f33c-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="1f33c-111">**Geen een SensorTag?:** [beginnen met een gesimuleerd apparaat](iot-hub-gateway-kit-c-sim-get-started.md) of [een SensorTag kopen](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="1f33c-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="1f33c-112">Les 1: Uw NUC configureren</span><span class="sxs-lookup"><span data-stu-id="1f33c-112">Lesson 1: Configure your NUC</span></span>
![Lesson1 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="1f33c-114">In deze les Intel NUC (volgende eenheid van computers) instellen in Hallo Kit als een Azure-IoT-gateway, hello Azure IoT rand pakket op NUC installeren en uitvoeren van een voorbeeld-app tooverify Hallo functionaliteit van de gateway.</span><span class="sxs-lookup"><span data-stu-id="1f33c-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="1f33c-115">*Geschatte tijd toocomplete: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="1f33c-116">Ga te[Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="1f33c-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="1f33c-117">Les 2: Uw IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="1f33c-117">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="1f33c-119">In deze les installeert u Hallo-hulpprogramma's en software op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="1f33c-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="1f33c-120">Vervolgens maken uw gratis Azure-account, het inrichten van uw Azure-IoT-hub en uw eerste apparaat maakt in Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="1f33c-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="1f33c-121">Les 1 voltooien voordat u deze les.</span><span class="sxs-lookup"><span data-stu-id="1f33c-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="1f33c-122">Hallo-hulpprogramma's ophalen</span><span class="sxs-lookup"><span data-stu-id="1f33c-122">Get hello tools</span></span>
<span data-ttu-id="1f33c-123">Hallo-hulpprogramma's en -software installeren op de hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="1f33c-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="1f33c-124">*Geschatte tijd toocomplete: 20 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="1f33c-125">Ga te[Hallo-hulpprogramma's ophalen](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="1f33c-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="1f33c-126">Een iothub maken en uw apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="1f33c-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="1f33c-127">Toevoegen van uw eerste apparaat toohello IoT-hub hello Azure CLI met uw resourcegroep maken en inrichten van uw eerste Azure-IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="1f33c-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="1f33c-128">*Geschatte tijd toocomplete: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="1f33c-129">Ga te[een iothub maken en uw apparaat registreren](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="1f33c-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="1f33c-130">Les 3: Berichten ontvangen van SensorTag en berichten lezen uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="1f33c-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="1f33c-131">In deze les gebruikt u scripts tooautomate Hallo configuratie en uitvoering van een voorbeeldtoepassing uitschakelen in uw gateway.</span><span class="sxs-lookup"><span data-stu-id="1f33c-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="1f33c-132">Dergelijke toepassingen gebruikt u een verzameling van gegevens voor het tooaggregate en transformatie van modules, verwerken van opdrachten of een willekeurig aantal gerelateerde taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f33c-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="1f33c-133">Modules communiceren met elkaar via een broker bericht.</span><span class="sxs-lookup"><span data-stu-id="1f33c-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="1f33c-134">Hallo-voorbeeldtoepassing heeft een module uitschakelen en een IoT hub-module.</span><span class="sxs-lookup"><span data-stu-id="1f33c-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="1f33c-135">Hallo uitschakelen module ontvangt gegevens van SensorTag uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="1f33c-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="1f33c-136">Hallo IoT hub module pakketten Hallo gegevens ontvangen en verzendt deze tooyour IoT-hub door Hallo gateway raamwerk geleverd in Azure IoT rand.</span><span class="sxs-lookup"><span data-stu-id="1f33c-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Les 3 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="1f33c-138">Configureren en Hallo uitschakelen voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1f33c-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="1f33c-139">Hallo-connectiviteit tussen SensorTag en uw gateway instellen.</span><span class="sxs-lookup"><span data-stu-id="1f33c-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="1f33c-140">Vervolgens Hallo-configuratie voltooien en Hallo uitschakelen voorbeeldtoepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f33c-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="1f33c-141">*Geschatte tijd toocomplete: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="1f33c-142">Ga te[voorbeeld-app uitvoeren Hallo inschakelen en configureren](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="1f33c-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="1f33c-143">Lezen van berichten uit uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="1f33c-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="1f33c-144">Voorbeeldcode uitvoeren op uw host computer tooread berichten uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="1f33c-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="1f33c-145">*Geschatte tijd toocomplete: 15 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="1f33c-146">Ga te[berichten lezen uit uw IoT-hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="1f33c-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="1f33c-147">Les 4: Berichten tooAzure Table storage opslaan</span><span class="sxs-lookup"><span data-stu-id="1f33c-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="1f33c-148">Maak een Azure-functie-app die binnenkomende berichten ontvangt van uw IoT-hub en schrijft deze tooAzure Table storage.</span><span class="sxs-lookup"><span data-stu-id="1f33c-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Les 4 end-to-end-diagram](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="1f33c-150">Een Azure-functie-app en Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="1f33c-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="1f33c-151">Een Azure-functie-app en een Azure Storage-account, kunt u een toocreate Azure Resource Manager-sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f33c-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="1f33c-152">*Geschatte tijd toocomplete: 10 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="1f33c-153">Ga te[een Azure-functie-app en Azure Storage-account maken](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="1f33c-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="1f33c-154">Alleen berichten permanent in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="1f33c-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="1f33c-155">Hallo gateway-naar-cloud-berichten bewaken tijdens deze tooAzure Table storage worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="1f33c-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="1f33c-156">*Geschatte tijd toocomplete: 5 minuten*</span><span class="sxs-lookup"><span data-stu-id="1f33c-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="1f33c-157">Ga te[gelezen berichten permanent in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1f33c-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1f33c-158">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="1f33c-158">Troubleshooting</span></span>
<span data-ttu-id="1f33c-159">Als u problemen tijdens Hallo uitkomsten hebt, zoekt u naar oplossingen in Hallo [probleemoplossing](iot-hub-gateway-kit-c-troubleshooting.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1f33c-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="1f33c-160">Meer verkennen</span><span class="sxs-lookup"><span data-stu-id="1f33c-160">Explore more</span></span>
<span data-ttu-id="1f33c-161">Ga naar Hallo [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="1f33c-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
