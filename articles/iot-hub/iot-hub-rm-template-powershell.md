---
title: aaaCreate een Azure-IoT-Hub met een sjabloon (PowerShell) | Microsoft Docs
description: Hoe toouse een Azure Resource Manager-sjabloon toocreate een IoT Hub met PowerShell.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="e3317-103">Een iothub met Azure Resource Manager-sjabloon (PowerShell) maken</span><span class="sxs-lookup"><span data-stu-id="e3317-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="e3317-104">U kunt Azure Resource Manager toocreate gebruiken en Azure IoT hubs programmatisch te beheren.</span><span class="sxs-lookup"><span data-stu-id="e3317-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="e3317-105">Deze zelfstudie leert u hoe toouse een Azure Resource Manager-sjabloon toocreate een iothub met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3317-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e3317-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e3317-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e3317-107">In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e3317-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="e3317-108">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3317-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e3317-109">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e3317-109">An active Azure account.</span></span> <br/><span data-ttu-id="e3317-110">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="e3317-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="e3317-111">[Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.</span><span class="sxs-lookup"><span data-stu-id="e3317-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="e3317-112">Hallo artikel [Azure PowerShell gebruiken met Azure Resource Manager] [ lnk-powershell-arm] vindt u meer informatie over het toouse PowerShell en Azure Resource Manager-sjablonen toocreate Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e3317-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="e3317-113">Verbinding maken met tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e3317-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="e3317-114">Voer in een PowerShell-opdrachtprompt Hallo opdracht toosign in tooyour Azure-abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3317-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e3317-115">Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="e3317-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="e3317-116">Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e3317-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="e3317-117">Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="e3317-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="e3317-118">U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e3317-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="e3317-119">Kunt u de volgende opdrachten toodiscover waarin u een IoT-hub kunt implementeren en API-versies die momenteel worden ondersteund door Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e3317-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="e3317-120">Maak een groep resource toocontain uw IoT-hub met behulp van de volgende opdracht in een van de locaties Hallo ondersteund voor IoT Hub Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3317-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="e3317-121">In dit voorbeeld maakt u een resourcegroep aangeroepen **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="e3317-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="e3317-122">Een sjabloon toocreate een IoT-hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="e3317-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="e3317-123">Gebruik een JSON-sjabloon toocreate een IoT-hub in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e3317-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="e3317-124">U kunt ook een Azure Resource Manager sjabloon toomake wijzigingen tooan iothub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e3317-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="e3317-125">Gebruik een tekst-editor toocreate aangeroepen voor een Azure Resource Manager-sjabloon **template.json** met Hallo volgende resource definition toocreate een nieuwe standaard IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="e3317-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="e3317-126">Dit voorbeeld wordt Hallo IoT-Hub in Hallo **VS-Oost** regio, maakt u twee consumergroepen (**cg1** en **cg2**) op Hallo Event Hub-compatibele eindpunt en maakt gebruik van Hallo **2016-02-03** API-versie.</span><span class="sxs-lookup"><span data-stu-id="e3317-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="e3317-127">Deze sjabloon ook verwacht u toopass in naam Hallo IoT-hub als een parameter met de naam **hubName**.</span><span class="sxs-lookup"><span data-stu-id="e3317-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="e3317-128">Zie voor de huidige lijst Hallo van locaties die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="e3317-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="e3317-129">Sla hello Azure Resource Manager-sjabloonbestand op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="e3317-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="e3317-130">In dit voorbeeld wordt ervan uitgegaan dat u deze opslaan in een map met de naam **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="e3317-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="e3317-131">Voer Hallo opdracht toodeploy na uw nieuwe IoT-hub Hallo-naam van uw IoT-hub wordt doorgegeven als parameter.</span><span class="sxs-lookup"><span data-stu-id="e3317-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="e3317-132">In dit voorbeeld is de naam van de Hallo van Hallo iothub `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="e3317-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="e3317-133">Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn:</span><span class="sxs-lookup"><span data-stu-id="e3317-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="e3317-134">Hallo-uitvoer geeft Hallo sleutels voor Hallo IoT-hub die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3317-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="e3317-135">uw toepassing toegevoegd tooverify nieuwe iothub, gaat u naar Hallo Hallo [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven.</span><span class="sxs-lookup"><span data-stu-id="e3317-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="e3317-136">Ook gebruiken Hallo **Get-AzureRmResource** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3317-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e3317-137">Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="e3317-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="e3317-138">U kunt IoT-hub via Hallo Hallo verwijderen [Azure-portal] [ lnk-azure-portal] of met behulp van Hallo **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="e3317-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3317-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3317-139">Next steps</span></span>

<span data-ttu-id="e3317-140">Nu u een iothub met een Azure Resource Manager-sjabloon met PowerShell hebt geïmplementeerd, kunt u verder tooexplore:</span><span class="sxs-lookup"><span data-stu-id="e3317-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="e3317-141">Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="e3317-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="e3317-142">Lees [overzicht van Azure Resource Manager] [ lnk-azure-rm-overview] toolearn meer over Hallo-mogelijkheden van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e3317-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="e3317-143">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3317-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="e3317-144">[Inleiding tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="e3317-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="e3317-145">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="e3317-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="e3317-146">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="e3317-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e3317-147">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e3317-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
