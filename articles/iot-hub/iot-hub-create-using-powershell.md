---
title: een Azure-IoT-Hub met een PowerShell-cmdlet aaaCreate | Microsoft Docs
description: Hoe toouse een PowerShell-cmdlet toocreate een IoT-hub.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="69a50-103">Een iothub met de cmdlet New-AzureRmIotHub Hallo maken</span><span class="sxs-lookup"><span data-stu-id="69a50-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="69a50-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="69a50-104">Introduction</span></span>

<span data-ttu-id="69a50-105">U kunt Azure PowerShell-cmdlets toocreate gebruiken en beheren van Azure IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="69a50-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="69a50-106">Deze zelfstudie leert u hoe toocreate een iothub met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69a50-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="69a50-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="69a50-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="69a50-108">In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="69a50-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="69a50-109">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="69a50-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="69a50-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="69a50-110">An active Azure account.</span></span> <br/><span data-ttu-id="69a50-111">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="69a50-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="69a50-112">[Azure PowerShell-cmdlets][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="69a50-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="69a50-113">Verbinding maken met tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="69a50-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="69a50-114">Voer in een PowerShell-opdrachtprompt Hallo opdracht toosign in tooyour Azure-abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="69a50-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="69a50-115">Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="69a50-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="69a50-116">Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="69a50-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="69a50-117">Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="69a50-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="69a50-118">U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="69a50-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="69a50-119">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="69a50-119">Create resource group</span></span>

<span data-ttu-id="69a50-120">U moet een resource groep toodeploy een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="69a50-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="69a50-121">U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="69a50-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="69a50-122">U kunt volgende opdracht toodiscover Hallo locaties waar u een IoT-hub kunt implementeren hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="69a50-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="69a50-123">een resourcegroep voor uw IoT-hub in een Hallo toocreate ondersteund locaties voor IoT Hub, gebruik Hallo na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="69a50-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="69a50-124">In dit voorbeeld maakt u een resourcegroep aangeroepen **MyIoTRG1** in Hallo **VS-Oost** regio:</span><span class="sxs-lookup"><span data-stu-id="69a50-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="69a50-125">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="69a50-125">Create an IoT hub</span></span>

<span data-ttu-id="69a50-126">toocreate een IoT-hub in Hallo-resourcegroep die u hebt gemaakt in Hallo vorige stap, gebruik Hallo volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="69a50-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="69a50-127">In dit voorbeeld wordt een **S1** hub aangeroepen **MyTestIoTHub** in Hallo **VS-Oost** regio:</span><span class="sxs-lookup"><span data-stu-id="69a50-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="69a50-128">Hallo-naam van de IoT-hub Hallo moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="69a50-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="69a50-129">U kunt alle Hallo IoT hubs in uw abonnement met behulp van de volgende opdracht Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="69a50-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="69a50-130">Hallo vorige voorbeeld wordt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="69a50-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="69a50-131">U kunt Hallo iothub met behulp van de volgende opdracht Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="69a50-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="69a50-132">U kunt ook kunt u een resourcegroep en alle resources die deze bevat met behulp van de volgende opdracht Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="69a50-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="69a50-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69a50-133">Next steps</span></span>

<span data-ttu-id="69a50-134">Nu u een iothub met een PowerShell-cmdlet hebt geïmplementeerd, kunt u verder tooexplore:</span><span class="sxs-lookup"><span data-stu-id="69a50-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="69a50-135">Detecteren van andere [PowerShell-cmdlets voor het werken met uw IoT-hub][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="69a50-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="69a50-136">Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="69a50-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="69a50-137">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="69a50-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="69a50-138">[Inleiding tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="69a50-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="69a50-139">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="69a50-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="69a50-140">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="69a50-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="69a50-141">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="69a50-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
