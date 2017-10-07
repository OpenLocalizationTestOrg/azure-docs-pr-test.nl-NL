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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Een iothub met Azure Resource Manager-sjabloon (PowerShell) maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

U kunt Azure Resource Manager toocreate gebruiken en Azure IoT hubs programmatisch te beheren. Deze zelfstudie leert u hoe toouse een Azure Resource Manager-sjabloon toocreate een iothub met PowerShell.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. <br/>Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.

> [!TIP]
> Hallo artikel [Azure PowerShell gebruiken met Azure Resource Manager] [ lnk-powershell-arm] vindt u meer informatie over het toouse PowerShell en Azure Resource Manager-sjablonen toocreate Azure resources.

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

Kunt u de volgende opdrachten toodiscover waarin u een IoT-hub kunt implementeren en API-versies die momenteel worden ondersteund door Hallo Hallo gebruiken:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Maak een groep resource toocontain uw IoT-hub met behulp van de volgende opdracht in een van de locaties Hallo ondersteund voor IoT Hub Hallo. In dit voorbeeld maakt u een resourcegroep aangeroepen **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Een sjabloon toocreate een IoT-hub te verzenden

Gebruik een JSON-sjabloon toocreate een IoT-hub in de resourcegroep. U kunt ook een Azure Resource Manager sjabloon toomake wijzigingen tooan iothub gebruiken.

1. Gebruik een tekst-editor toocreate aangeroepen voor een Azure Resource Manager-sjabloon **template.json** met Hallo volgende resource definition toocreate een nieuwe standaard IoT-hub. Dit voorbeeld wordt Hallo IoT-Hub in Hallo **VS-Oost** regio, maakt u twee consumergroepen (**cg1** en **cg2**) op Hallo Event Hub-compatibele eindpunt en maakt gebruik van Hallo **2016-02-03** API-versie. Deze sjabloon ook verwacht u toopass in naam Hallo IoT-hub als een parameter met de naam **hubName**. Zie voor de huidige lijst Hallo van locaties die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status].

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

2. Sla hello Azure Resource Manager-sjabloonbestand op uw lokale machine. In dit voorbeeld wordt ervan uitgegaan dat u deze opslaan in een map met de naam **c:\templates**.

3. Voer Hallo opdracht toodeploy na uw nieuwe IoT-hub Hallo-naam van uw IoT-hub wordt doorgegeven als parameter. In dit voorbeeld is de naam van de Hallo van Hallo iothub `abcmyiothub`. Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. Hallo-uitvoer geeft Hallo sleutels voor Hallo IoT-hub die u hebt gemaakt.

5. uw toepassing toegevoegd tooverify nieuwe iothub, gaat u naar Hallo Hallo [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven. Ook gebruiken Hallo **Get-AzureRmResource** PowerShell-cmdlet.

> [!NOTE]
> Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd. U kunt IoT-hub via Hallo Hallo verwijderen [Azure-portal] [ lnk-azure-portal] of met behulp van Hallo **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.

## <a name="next-steps"></a>Volgende stappen

Nu u een iothub met een Azure Resource Manager-sjabloon met PowerShell hebt geïmplementeerd, kunt u verder tooexplore:

* Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].
* Lees [overzicht van Azure Resource Manager] [ lnk-azure-rm-overview] toolearn meer over Hallo-mogelijkheden van Azure Resource Manager.

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:

* [Inleiding tooC SDK][lnk-c-sdk]
* [Azure IoT SDK 's][lnk-sdks]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

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
