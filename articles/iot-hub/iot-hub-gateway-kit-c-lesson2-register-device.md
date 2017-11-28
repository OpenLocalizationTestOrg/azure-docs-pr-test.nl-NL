---
title: 'SensorTag apparaat & Azure IoT Gateway - les 2: apparaat registreren | Microsoft Docs'
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iothub, internet van dingen cloud azure iothub maken apparaat, ti sensortag, ti uitschakelen
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="4d45d-103">Maken van uw Azure-IoT-hub en Registreer uw apparaat</span><span class="sxs-lookup"><span data-stu-id="4d45d-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4d45d-104">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="4d45d-104">What you will do</span></span>

- <span data-ttu-id="4d45d-105">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="4d45d-105">Create a resource group</span></span>
- <span data-ttu-id="4d45d-106">Uw eerste IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="4d45d-106">Create your first IoT hub</span></span>
- <span data-ttu-id="4d45d-107">Registreer uw apparaat in uw iothub met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4d45d-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="4d45d-108">Wanneer u uw apparaat in uw IoT-hub registreren, genereert Hallo service Azure IoT Hub een sleutel voor uw apparaat toouse tooauthenticate met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="4d45d-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="4d45d-109">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4d45d-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4d45d-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4d45d-110">What you will learn</span></span>

<span data-ttu-id="4d45d-111">In deze les leert u het:</span><span class="sxs-lookup"><span data-stu-id="4d45d-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="4d45d-112">Hoe toouse hello Azure CLI toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="4d45d-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="4d45d-113">Hoe tooregister een apparaat in een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="4d45d-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4d45d-114">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="4d45d-114">What you need</span></span>

- <span data-ttu-id="4d45d-115">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4d45d-115">An active Azure subscription.</span></span> <span data-ttu-id="4d45d-116">Als u geen Azure-account hebt, kunt u een [gratis proefaccount voor Azure](http://azure.microsoft.com/pricing/free-trial/) over een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="4d45d-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="4d45d-117">U hebt hello die Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4d45d-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="4d45d-118">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="4d45d-118">Create an IoT hub</span></span>

<span data-ttu-id="4d45d-119">een IoT-hub toocreate als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="4d45d-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="4d45d-120">Meld u aan tooyour Azure-account door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="4d45d-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="4d45d-121">Alle beschikbare abonnementen worden weergegeven na een geslaagde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="4d45d-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="4d45d-122">Hallo standaard Azure-abonnement dat u door het uitvoeren van de volgende opdracht Hallo toouse wilt instellen:</span><span class="sxs-lookup"><span data-stu-id="4d45d-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="4d45d-123">`subscription ID or name`kunt u vinden in de uitvoer van Hallo Hallo `az login` of Hallo `az account list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="4d45d-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="4d45d-124">Hallo-provider door het uitvoeren van de volgende opdracht Hallo registreren.</span><span class="sxs-lookup"><span data-stu-id="4d45d-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="4d45d-125">Resourceproviders zijn services die bronnen voor uw toepassing bieden.</span><span class="sxs-lookup"><span data-stu-id="4d45d-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="4d45d-126">Voordat u Azure-resource die provider aanbiedingen Hallo Hallo kunt implementeren, moet u Hallo provider registreren.</span><span class="sxs-lookup"><span data-stu-id="4d45d-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="4d45d-127">Maak een resourcegroep met de naam `iot-gateway` in de regio VS-West Hallo door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="4d45d-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="4d45d-128">`westus`Hallo locatie maken van de resourcegroep is.</span><span class="sxs-lookup"><span data-stu-id="4d45d-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="4d45d-129">Als u wilt dat toouse een andere locatie, kunt u uitvoeren `az account list-locations -o table` toosee alle Hallo locaties Azure ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="4d45d-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="4d45d-130">Maken van een IoT-hub in Hallo `iot-gateway` resourcegroep door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="4d45d-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="4d45d-131">Hallo hulpprogramma maakt standaard een IoT-Hub in de gratis prijscategorie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4d45d-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="4d45d-132">Zie voor meer informatie [prijzen van Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="4d45d-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="4d45d-133">Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="4d45d-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="4d45d-134">U kunt slechts één F1-editie van Azure Iot Hub maken onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4d45d-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="4d45d-135">Registreer uw apparaat bij uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="4d45d-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="4d45d-136">Elk apparaat dat berichten tooyour iothub verzendt en ontvangt berichten van uw IoT-hub moet zijn geregistreerd met een unieke ID.</span><span class="sxs-lookup"><span data-stu-id="4d45d-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="4d45d-137">Registreer uw apparaat in uw IoT-hub door met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4d45d-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="4d45d-138">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4d45d-138">Summary</span></span>

<span data-ttu-id="4d45d-139">U hebt een IoT-hub gemaakt en het logische apparaat geregistreerd bij een apparaat-id in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="4d45d-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="4d45d-140">U bent klaar toolearn hoe tooconfigure en voer een gateway toepassing toosend voorbeeldgegevens van uw fysieke apparaat tooyour IoT-hub in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="4d45d-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d45d-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d45d-141">Next steps</span></span>
[<span data-ttu-id="4d45d-142">Configureren en uitvoeren van een voorbeeldapp uitschakelen</span><span class="sxs-lookup"><span data-stu-id="4d45d-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)