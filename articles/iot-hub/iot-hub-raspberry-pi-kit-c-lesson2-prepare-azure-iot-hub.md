---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en registreren Pi in hello Azure IoT hub met behulp van hello Azure CLI.
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
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="486f9-104">Het maken van uw IoT-hub en frambozen Pi 3 registreren</span><span class="sxs-lookup"><span data-stu-id="486f9-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="486f9-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="486f9-105">What you will do</span></span>
* <span data-ttu-id="486f9-106">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="486f9-106">Create a resource group.</span></span>
* <span data-ttu-id="486f9-107">Uw Azure-IoT-hub in de resourcegroep Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="486f9-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="486f9-108">Frambozen Pi 3 toohello Azure IoT hub toevoegen met behulp van hello Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="486f9-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="486f9-109">Wanneer u hello Azure CLI tooadd Pi tooyour iothub, genereert Hallo-service een sleutel voor Pi tooauthenticate met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="486f9-109">When you use hello Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="486f9-110">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="486f9-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="486f9-111">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="486f9-111">What you will learn</span></span>
<span data-ttu-id="486f9-112">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="486f9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="486f9-113">Hoe toouse hello Azure CLI toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="486f9-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="486f9-114">Hoe toocreate een apparaat-id voor Pi in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="486f9-114">How toocreate a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="486f9-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="486f9-115">What you need</span></span>
* <span data-ttu-id="486f9-116">Een Azure-account</span><span class="sxs-lookup"><span data-stu-id="486f9-116">An Azure account</span></span>
* <span data-ttu-id="486f9-117">Een Mac- of een computer met Windows Hello Azure CLI is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="486f9-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="486f9-118">Maken van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="486f9-118">Create your IoT hub</span></span>
<span data-ttu-id="486f9-119">Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa.</span><span class="sxs-lookup"><span data-stu-id="486f9-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="486f9-120">toocreate uw IoT-hub als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="486f9-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="486f9-121">Meld u aan tooyour Azure-account door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="486f9-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="486f9-122">Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="486f9-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="486f9-123">Hallo standaardabonnement die u door het uitvoeren van de volgende opdracht Hallo toouse wilt instellen:</span><span class="sxs-lookup"><span data-stu-id="486f9-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="486f9-124">`subscription ID or name`kunt u vinden in de uitvoer van Hallo Hallo `az login` of Hallo `az account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="486f9-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="486f9-125">Hallo-provider door het uitvoeren van de volgende opdracht Hallo registreren.</span><span class="sxs-lookup"><span data-stu-id="486f9-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="486f9-126">Resourceproviders zijn services die bronnen voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="486f9-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="486f9-127">Voordat u Azure-resource die provider aanbiedingen Hallo Hallo kunt implementeren, moet u Hallo provider registreren.</span><span class="sxs-lookup"><span data-stu-id="486f9-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="486f9-128">Maak een resourcegroep met de naam iot-sample in de regio VS-West Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="486f9-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="486f9-129">`westus`Hallo locatie maken van de resourcegroep is.</span><span class="sxs-lookup"><span data-stu-id="486f9-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="486f9-130">Als u wilt dat toouse een andere locatie, kunt u uitvoeren `az account list-locations -o table` toosee alle Hallo locaties Azure ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="486f9-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="486f9-131">Een iothub in Hallo iot-sample resourcegroep maken door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="486f9-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="486f9-132">Hallo hulpprogramma maakt standaard een IoT-Hub in de gratis prijscategorie Hallo.</span><span class="sxs-lookup"><span data-stu-id="486f9-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="486f9-133">Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="486f9-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="486f9-134">Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="486f9-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="486f9-135">U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="486f9-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="486f9-136">Pi registreren in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="486f9-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="486f9-137">Elk apparaat dat berichten tooyour iothub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.</span><span class="sxs-lookup"><span data-stu-id="486f9-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="486f9-138">Registreren Pi in uw hub door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="486f9-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="486f9-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="486f9-139">Summary</span></span>
<span data-ttu-id="486f9-140">U hebt een IoT-hub gemaakt en geregistreerd Pi met een apparaat-id in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="486f9-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="486f9-141">U bent klaar toolearn hoe toosend uit Pi tooyour iothub berichten.</span><span class="sxs-lookup"><span data-stu-id="486f9-141">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="486f9-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="486f9-142">Next steps</span></span>
<span data-ttu-id="486f9-143">[Maak een Azure-functie-app en een Azure Storage-account tooprocess en store IoT-hub berichten](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="486f9-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

