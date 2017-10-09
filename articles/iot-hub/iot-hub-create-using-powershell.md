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
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Een iothub met de cmdlet New-AzureRmIotHub Hallo maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Inleiding

U kunt Azure PowerShell-cmdlets toocreate gebruiken en beheren van Azure IoT hubs. Deze zelfstudie leert u hoe toocreate een iothub met PowerShell.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. <br/>Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure PowerShell-cmdlets][lnk-powershell-install].

## <a name="connect-tooyour-azure-subscription"></a>Verbinding maken met tooyour Azure-abonnement
Voer in een PowerShell-opdrachtprompt Hallo opdracht toosign in tooyour Azure-abonnement te volgen:

```powershell
Login-AzureRmAccount
```

Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt. Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:

```powershell
Get-AzureRMSubscription
```

Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen. U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a>Een resourcegroep maken

U moet een resource groep toodeploy een IoT-hub. U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.

U kunt volgende opdracht toodiscover Hallo locaties waar u een IoT-hub kunt implementeren hello gebruiken:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

een resourcegroep voor uw IoT-hub in een Hallo toocreate ondersteund locaties voor IoT Hub, gebruik Hallo na de opdracht. In dit voorbeeld maakt u een resourcegroep aangeroepen **MyIoTRG1** in Hallo **VS-Oost** regio:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Een IoT Hub maken

toocreate een IoT-hub in Hallo-resourcegroep die u hebt gemaakt in Hallo vorige stap, gebruik Hallo volgende opdracht. In dit voorbeeld wordt een **S1** hub aangeroepen **MyTestIoTHub** in Hallo **VS-Oost** regio:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

Hallo-naam van de IoT-hub Hallo moet uniek zijn.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


U kunt alle Hallo IoT hubs in uw abonnement met behulp van de volgende opdracht Hallo weergeven:

```powershell
Get-AzureRmIotHub
```

Hallo vorige voorbeeld wordt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd. U kunt Hallo iothub met behulp van de volgende opdracht Hallo verwijderen:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

U kunt ook kunt u een resourcegroep en alle resources die deze bevat met behulp van de volgende opdracht Hallo Hallo:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Volgende stappen

Nu u een iothub met een PowerShell-cmdlet hebt geïmplementeerd, kunt u verder tooexplore:

* Detecteren van andere [PowerShell-cmdlets voor het werken met uw IoT-hub][lnk-iothub-cmdlets].
* Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:

* [Inleiding tooC SDK][lnk-c-sdk]
* [Azure IoT SDK 's][lnk-sdks]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met IoT rand][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
