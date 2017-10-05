---
featureFlags: usabilla
title: 'Frambozen Pi (knooppunt) verbinden met Azure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en Pi registreren in het identiteitenregister van IoT Hub met behulp van Azure CLI.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: verbinding maken Raspberry pi cloud, pi-cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="44a46-104">Het maken van uw IoT-hub en frambozen Pi 3 registreren</span><span class="sxs-lookup"><span data-stu-id="44a46-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="44a46-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="44a46-105">What you will do</span></span>
* <span data-ttu-id="44a46-106">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="44a46-106">Create a resource group.</span></span>
* <span data-ttu-id="44a46-107">Uw Azure-IoT-hub in de resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="44a46-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="44a46-108">Frambozen Pi 3 toevoegen aan de Azure IoT hub met behulp van de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="44a46-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="44a46-109">Wanneer u Azure CLI Pi toevoegen aan uw IoT-hub, genereert de service een sleutel voor Pi voor verificatie met de service.</span><span class="sxs-lookup"><span data-stu-id="44a46-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="44a46-110">Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="44a46-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="44a46-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="44a46-111">What you will learn</span></span>
<span data-ttu-id="44a46-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="44a46-112">In this article, you will learn:</span></span>
* <span data-ttu-id="44a46-113">Het gebruik van Azure CLI voor een iothub maken</span><span class="sxs-lookup"><span data-stu-id="44a46-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="44a46-114">Het maken van een apparaat-id voor Pi in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="44a46-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="44a46-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="44a46-115">What you need</span></span>
* <span data-ttu-id="44a46-116">Een Azure-account</span><span class="sxs-lookup"><span data-stu-id="44a46-116">An Azure account</span></span>
* <span data-ttu-id="44a46-117">Een Mac- of een Windows-computer met de Azure CLI geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="44a46-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="44a46-118">Maken van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="44a46-118">Create your IoT hub</span></span>
<span data-ttu-id="44a46-119">Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa.</span><span class="sxs-lookup"><span data-stu-id="44a46-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="44a46-120">Volg deze stappen voor het maken van uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="44a46-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="44a46-121">Meld u aan bij uw Azure-account met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44a46-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="44a46-122">Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="44a46-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="44a46-123">Stel de standaardabonnement dat u gebruiken wilt met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44a46-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="44a46-124">`subscription ID or name`kunt u vinden in de uitvoer van de `az login` of de `az account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="44a46-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="44a46-125">Registreer de provider door de volgende opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="44a46-125">Register the provider by running the following command.</span></span> <span data-ttu-id="44a46-126">Resourceproviders zijn services die bronnen voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="44a46-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="44a46-127">Voordat u de Azure-resource die de provider biedt kunt implementeren, moet u de provider registreren.</span><span class="sxs-lookup"><span data-stu-id="44a46-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="44a46-128">Maak een resourcegroep met de iot-voorbeeld in de regio VS-West naam door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="44a46-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="44a46-129">`westus`is de locatie die u maakt de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="44a46-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="44a46-130">Als u gebruiken van een andere locatie wilt, kunt u uitvoeren `az account list-locations -o table` voor een overzicht van alle locaties Azure ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="44a46-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="44a46-131">Een iothub in de iot-sample resourcegroep maken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44a46-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="44a46-132">Het hulpprogramma maakt standaard een IoT-Hub in de prijscategorie gratis.</span><span class="sxs-lookup"><span data-stu-id="44a46-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="44a46-133">Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="44a46-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="44a46-134">De naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="44a46-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="44a46-135">U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="44a46-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="44a46-136">Pi registreren in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="44a46-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="44a46-137">Elk apparaat dat berichten naar uw IoT-hub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.</span><span class="sxs-lookup"><span data-stu-id="44a46-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="44a46-138">U kunt Azure CLI uw Pi registreren en maak een zelfondertekend X.509-certificaat voor verificatie van apparaten.</span><span class="sxs-lookup"><span data-stu-id="44a46-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="44a46-139">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="44a46-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="44a46-140">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="44a46-140">Summary</span></span>
<span data-ttu-id="44a46-141">U hebt een IoT-hub gemaakt en geregistreerd Pi met een apparaat-id in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="44a46-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="44a46-142">U kunt meer informatie over het verzenden van berichten vanaf Pi naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="44a46-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44a46-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44a46-143">Next steps</span></span>
[<span data-ttu-id="44a46-144">Maak een Azure-functie-app en een Azure storage-account om te verwerken en IoT hub berichten opslaan</span><span class="sxs-lookup"><span data-stu-id="44a46-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

