---
title: 'Connect Intel Edison (C) naar Azure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en Edison registreren in de Azure IoT hub met behulp van de Azure CLI.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="8364c-103">Het maken van uw IoT-hub en Intel Edison registreren</span><span class="sxs-lookup"><span data-stu-id="8364c-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8364c-104">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="8364c-104">What you will do</span></span>
* <span data-ttu-id="8364c-105">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8364c-105">Create a resource group.</span></span>
* <span data-ttu-id="8364c-106">Uw Azure-IoT-hub in de resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="8364c-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="8364c-107">Intel Edison toevoegen aan de Azure IoT hub met behulp van de Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="8364c-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="8364c-108">Wanneer u de Azure CLI Edison toevoegen aan uw IoT-hub, genereert de service een sleutel voor Edison voor verificatie met de service.</span><span class="sxs-lookup"><span data-stu-id="8364c-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="8364c-109">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8364c-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8364c-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="8364c-110">What you will learn</span></span>
<span data-ttu-id="8364c-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="8364c-111">In this article, you will learn:</span></span>
* <span data-ttu-id="8364c-112">Het gebruik van de Azure CLI voor het maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8364c-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="8364c-113">Het maken van een apparaat-id voor Edison in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8364c-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8364c-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8364c-114">What you need</span></span>
* <span data-ttu-id="8364c-115">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8364c-115">An Azure account.</span></span> <span data-ttu-id="8364c-116">Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="8364c-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="8364c-117">U moet de Azure CLI geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="8364c-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="8364c-118">Maken van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="8364c-118">Create your IoT hub</span></span>
<span data-ttu-id="8364c-119">Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa.</span><span class="sxs-lookup"><span data-stu-id="8364c-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="8364c-120">Volg deze stappen voor het maken van uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="8364c-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="8364c-121">Meld u aan bij uw Azure-account met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8364c-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="8364c-122">Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="8364c-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="8364c-123">Stel de standaardabonnement dat u gebruiken wilt met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8364c-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="8364c-124">`subscription ID or name`kunt u vinden in de uitvoer van de `az login` of de `az account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8364c-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="8364c-125">Registreer de provider door de volgende opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8364c-125">Register the provider by running the following command.</span></span> <span data-ttu-id="8364c-126">Resourceproviders zijn services die bronnen voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="8364c-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="8364c-127">Voordat u de Azure-resource die de provider biedt kunt implementeren, moet u de provider registreren.</span><span class="sxs-lookup"><span data-stu-id="8364c-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="8364c-128">Maak een resourcegroep met de iot-voorbeeld in de regio VS-West naam door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="8364c-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="8364c-129">`westus`is de locatie die u maakt de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8364c-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="8364c-130">Als u gebruiken van een andere locatie wilt, kunt u uitvoeren `az account list-locations -o table` voor een overzicht van alle locaties Azure ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="8364c-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="8364c-131">Een iothub in de iot-sample resourcegroep maken met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8364c-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="8364c-132">Het hulpprogramma maakt standaard een IoT-Hub in de prijscategorie gratis.</span><span class="sxs-lookup"><span data-stu-id="8364c-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="8364c-133">Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="8364c-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="8364c-134">De naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="8364c-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="8364c-135">U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8364c-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="8364c-136">Edison registreren in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="8364c-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="8364c-137">Elk apparaat dat berichten naar uw IoT-hub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.</span><span class="sxs-lookup"><span data-stu-id="8364c-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="8364c-138">Registreren Edison in uw IoT-hub door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8364c-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="8364c-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8364c-139">Summary</span></span>
<span data-ttu-id="8364c-140">U hebt een IoT-hub gemaakt en geregistreerd Edison met een apparaat-id in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8364c-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="8364c-141">U kunt meer informatie over het verzenden van berichten vanaf Edison naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8364c-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8364c-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8364c-142">Next steps</span></span>
<span data-ttu-id="8364c-143">[Maak een Azure-functie-app en een Azure Storage-account om te verwerken en opslaan van IoT hub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="8364c-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md