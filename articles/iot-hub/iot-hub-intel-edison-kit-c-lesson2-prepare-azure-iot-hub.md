---
title: 'Connect Intel Edison (C) tooAzure IoT - les 2: apparaat registreren | Microsoft Docs'
description: Een resourcegroep maken, een Azure IoT hub maken en registreren Edison in hello Azure IoT hub met behulp van hello Azure CLI.
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
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="873f1-103">Het maken van uw IoT-hub en Intel Edison registreren</span><span class="sxs-lookup"><span data-stu-id="873f1-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="873f1-104">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="873f1-104">What you will do</span></span>
* <span data-ttu-id="873f1-105">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="873f1-105">Create a resource group.</span></span>
* <span data-ttu-id="873f1-106">Uw Azure-IoT-hub in de resourcegroep Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="873f1-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="873f1-107">Intel Edison toohello Azure IoT hub toevoegen met behulp van hello Azure-opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="873f1-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="873f1-108">Wanneer u hello Azure CLI tooadd Edison tooyour iothub, genereert Hallo-service een sleutel voor Edison tooauthenticate met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="873f1-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="873f1-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="873f1-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="873f1-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="873f1-110">What you will learn</span></span>
<span data-ttu-id="873f1-111">In dit artikel leert u het:</span><span class="sxs-lookup"><span data-stu-id="873f1-111">In this article, you will learn:</span></span>
* <span data-ttu-id="873f1-112">Hoe toouse hello Azure CLI toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="873f1-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="873f1-113">Hoe toocreate een apparaat-id voor Edison in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="873f1-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="873f1-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="873f1-114">What you need</span></span>
* <span data-ttu-id="873f1-115">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="873f1-115">An Azure account.</span></span> <span data-ttu-id="873f1-116">Als u geen Azure-account hebt, maakt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="873f1-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="873f1-117">U hebt hello die Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="873f1-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="873f1-118">Maken van uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="873f1-118">Create your IoT hub</span></span>
<span data-ttu-id="873f1-119">Azure IoT-Hub kunt u verbinding maken, bewaken en beheren van miljoenen IoT activa.</span><span class="sxs-lookup"><span data-stu-id="873f1-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="873f1-120">toocreate uw IoT-hub als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="873f1-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="873f1-121">Meld u aan tooyour Azure-account door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="873f1-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="873f1-122">Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="873f1-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="873f1-123">Hallo standaardabonnement die u door het uitvoeren van de volgende opdracht Hallo toouse wilt instellen:</span><span class="sxs-lookup"><span data-stu-id="873f1-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="873f1-124">`subscription ID or name`kunt u vinden in de uitvoer van Hallo Hallo `az login` of Hallo `az account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="873f1-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="873f1-125">Hallo-provider door het uitvoeren van de volgende opdracht Hallo registreren.</span><span class="sxs-lookup"><span data-stu-id="873f1-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="873f1-126">Resourceproviders zijn services die bronnen voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="873f1-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="873f1-127">Voordat u Azure-resource die provider aanbiedingen Hallo Hallo kunt implementeren, moet u Hallo provider registreren.</span><span class="sxs-lookup"><span data-stu-id="873f1-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="873f1-128">Maak een resourcegroep met de naam iot-sample in de regio VS-West Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="873f1-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="873f1-129">`westus`Hallo locatie maken van de resourcegroep is.</span><span class="sxs-lookup"><span data-stu-id="873f1-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="873f1-130">Als u wilt dat toouse een andere locatie, kunt u uitvoeren `az account list-locations -o table` toosee alle Hallo locaties Azure ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="873f1-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="873f1-131">Een iothub in Hallo iot-sample resourcegroep maken door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="873f1-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="873f1-132">Hallo hulpprogramma maakt standaard een IoT-Hub in de gratis prijscategorie Hallo.</span><span class="sxs-lookup"><span data-stu-id="873f1-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="873f1-133">Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="873f1-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="873f1-134">Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="873f1-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="873f1-135">U kunt slechts één F1-editie van Azure IoT Hub maken onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="873f1-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="873f1-136">Edison registreren in uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="873f1-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="873f1-137">Elk apparaat dat berichten tooyour iothub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.</span><span class="sxs-lookup"><span data-stu-id="873f1-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="873f1-138">Registreren Edison in uw IoT-hub door het uitvoeren van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="873f1-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="873f1-139">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="873f1-139">Summary</span></span>
<span data-ttu-id="873f1-140">U hebt een IoT-hub gemaakt en geregistreerd Edison met een apparaat-id in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="873f1-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="873f1-141">U bent klaar toolearn hoe toosend uit Edison tooyour iothub berichten.</span><span class="sxs-lookup"><span data-stu-id="873f1-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="873f1-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="873f1-142">Next steps</span></span>
<span data-ttu-id="873f1-143">[Maak een Azure-functie-app en een Azure Storage-account tooprocess en store IoT-hub berichten][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="873f1-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md