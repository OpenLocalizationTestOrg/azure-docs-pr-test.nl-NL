---
title: 'Connect Raspberry PI (C) naar Azure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en Pi registreren in de Azure IoT hub met behulp van de Azure CLI.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: verbinding maken Raspberry pi cloud, pi-cloud
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
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="d3204-104">Het maken van uw IoT-hub en frambozen Pi 3 registreren</span><span class="sxs-lookup"><span data-stu-id="d3204-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d3204-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="d3204-105">What you will do</span></span>
* <span data-ttu-id="d3204-106">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d3204-106">Create a resource group.</span></span>
* <span data-ttu-id="d3204-107">Uw Azure-IoT-hub in de resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="d3204-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="d3204-108">Frambozen Pi 3 toevoegen aan de Azure IoT hub met behulp van de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="d3204-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="d3204-109">Wanneer u de Azure CLI Pi toevoegen aan uw IoT-hub, genereert de service een sleutel voor Pi voor verificatie met de service.</span><span class="sxs-lookup"><span data-stu-id="d3204-109">When you use the Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="d3204-110">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d3204-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d3204-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="d3204-111">What you will learn</span></span>
<span data-ttu-id="d3204-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="d3204-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d3204-113">Het gebruik van de Azure CLI voor het maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d3204-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="d3204-114">Het maken van een apparaat-id voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d3204-114">How to create a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d3204-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="d3204-115">What you need</span></span>
* <span data-ttu-id="d3204-116">Een Azure-account</span><span class="sxs-lookup"><span data-stu-id="d3204-116">An Azure account</span></span>
* <span data-ttu-id="d3204-117">Een Mac- of een Windows-computer met de Azure CLI geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="d3204-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="d3204-118">Maken van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="d3204-118">Create your IoT hub</span></span>
<span data-ttu-id="d3204-119">Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa.</span><span class="sxs-lookup"><span data-stu-id="d3204-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="d3204-120">Volg deze stappen voor het maken van uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="d3204-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="d3204-121">Meld u aan bij uw Azure-account met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d3204-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="d3204-122">Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="d3204-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="d3204-123">Stel de standaardabonnement dat u gebruiken wilt met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d3204-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="d3204-124">`subscription ID or name`kunt u vinden in de uitvoer van de `az login` of de `az account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="d3204-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="d3204-125">Registreer de provider door de volgende opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d3204-125">Register the provider by running the following command.</span></span> <span data-ttu-id="d3204-126">Resourceproviders zijn services die bronnen voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="d3204-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="d3204-127">Voordat u de Azure-resource die de provider biedt kunt implementeren, moet u de provider registreren.</span><span class="sxs-lookup"><span data-stu-id="d3204-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="d3204-128">Maak een resourcegroep met de iot-voorbeeld in de regio VS-West naam door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="d3204-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="d3204-129">`westus`is de locatie die u maakt de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="d3204-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="d3204-130">Als u gebruiken van een andere locatie wilt, kunt u uitvoeren `az account list-locations -o table` voor een overzicht van alle locaties Azure ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="d3204-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="d3204-131">Een iothub in de iot-sample resourcegroep maken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d3204-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="d3204-132">Het hulpprogramma maakt standaard een IoT-Hub in de prijscategorie gratis.</span><span class="sxs-lookup"><span data-stu-id="d3204-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="d3204-133">Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="d3204-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="d3204-134">De naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="d3204-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="d3204-135">U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d3204-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="d3204-136">Pi registreren in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="d3204-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="d3204-137">Elk apparaat dat berichten naar uw IoT-hub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.</span><span class="sxs-lookup"><span data-stu-id="d3204-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="d3204-138">Registreren Pi in uw hub door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d3204-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="d3204-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d3204-139">Summary</span></span>
<span data-ttu-id="d3204-140">U hebt een IoT-hub gemaakt en geregistreerd Pi met een apparaat-id in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d3204-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="d3204-141">U kunt meer informatie over het verzenden van berichten vanaf Pi naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d3204-141">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3204-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3204-142">Next steps</span></span>
<span data-ttu-id="d3204-143">[Maak een Azure-functie-app en een Azure Storage-account om te verwerken en opslaan van IoT hub berichten](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d3204-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

