---
title: Een Azure-IoT-Hub met een PowerShell-cmdlet maken | Microsoft Docs
description: Het gebruik van een PowerShell-cmdlet voor het maken van een IoT-hub.
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
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="e975e-103">Een iothub met de cmdlet New-AzureRmIotHub maken</span><span class="sxs-lookup"><span data-stu-id="e975e-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="e975e-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="e975e-104">Introduction</span></span>

<span data-ttu-id="e975e-105">U kunt Azure PowerShell-cmdlets gebruiken om te maken en beheren van Azure IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="e975e-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="e975e-106">Deze zelfstudie laat zien hoe u een IoT-hub maken met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e975e-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e975e-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e975e-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e975e-108">In dit artikel wordt behandeld met het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e975e-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="e975e-109">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="e975e-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e975e-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e975e-110">An active Azure account.</span></span> <br/><span data-ttu-id="e975e-111">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="e975e-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="e975e-112">[Azure PowerShell-cmdlets][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="e975e-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="e975e-113">Verbinding maken met uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e975e-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="e975e-114">Voer de volgende opdracht aan te melden bij uw Azure-abonnement in een PowerShell-opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="e975e-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e975e-115">Als u meerdere Azure-abonnementen hebt, verleent aanmelden bij Azure u toegang tot alle de Azure-abonnementen die zijn gekoppeld aan uw referenties.</span><span class="sxs-lookup"><span data-stu-id="e975e-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="e975e-116">Gebruik de volgende opdracht voor een lijst met de Azure-abonnementen beschikbaar moet worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="e975e-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="e975e-117">Gebruik de volgende opdracht om abonnement die u gebruiken wilt voor het uitvoeren van de opdrachten voor het maken van uw IoT-hub te selecteren.</span><span class="sxs-lookup"><span data-stu-id="e975e-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="e975e-118">U kunt de naam van abonnement of de ID van de uitvoer van de vorige opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e975e-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="e975e-119">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="e975e-119">Create resource group</span></span>

<span data-ttu-id="e975e-120">U moet een resourcegroep voor het implementeren van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="e975e-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="e975e-121">U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="e975e-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="e975e-122">U kunt de volgende opdracht gebruiken voor het detecteren van de locaties waar u een IoT-hub kunt implementeren:</span><span class="sxs-lookup"><span data-stu-id="e975e-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="e975e-123">Gebruik de volgende opdracht voor het maken van een resourcegroep voor uw IoT-hub in een van de ondersteunde locaties voor IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e975e-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="e975e-124">In dit voorbeeld maakt u een resourcegroep aangeroepen **MyIoTRG1** in de **VS-Oost** regio:</span><span class="sxs-lookup"><span data-stu-id="e975e-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="e975e-125">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="e975e-125">Create an IoT hub</span></span>

<span data-ttu-id="e975e-126">Voor het maken van een IoT-hub in de resourcegroep die u in de vorige stap hebt gemaakt, moet u de volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e975e-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="e975e-127">In dit voorbeeld wordt een **S1** hub aangeroepen **MyTestIoTHub** in de **VS-Oost** regio:</span><span class="sxs-lookup"><span data-stu-id="e975e-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="e975e-128">De naam van de IoT-hub moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="e975e-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="e975e-129">U kunt alle IoT-hubs weergeven in uw abonnement met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e975e-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="e975e-130">Het vorige voorbeeld wordt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="e975e-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="e975e-131">U kunt de iothub met de volgende opdracht verwijderen:</span><span class="sxs-lookup"><span data-stu-id="e975e-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="e975e-132">U kunt ook kunt u een resourcegroep en alle resources die deze bevat de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e975e-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="e975e-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e975e-133">Next steps</span></span>

<span data-ttu-id="e975e-134">Nu u een iothub met een PowerShell-cmdlet hebt geïmplementeerd, kunt u verder verkennen:</span><span class="sxs-lookup"><span data-stu-id="e975e-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="e975e-135">Detecteren van andere [PowerShell-cmdlets voor het werken met uw IoT-hub][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="e975e-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="e975e-136">Meer informatie over de mogelijkheden van de [resourceprovider IoT Hub REST-API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="e975e-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="e975e-137">Zie de volgende artikelen voor meer informatie over het ontwikkelen voor IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="e975e-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="e975e-138">[Inleiding tot C-SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="e975e-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="e975e-139">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="e975e-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="e975e-140">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="e975e-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e975e-141">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e975e-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
