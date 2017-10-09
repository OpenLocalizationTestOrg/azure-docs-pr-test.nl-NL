---
title: aaaControl Routering en virtuele apparaten via Azure CLI 2.0 Hallo | Microsoft Docs
description: Meer informatie over hoe toocontrol Routering en virtuele apparaten via Azure CLI 2.0 Hallo.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Door de gebruiker gedefinieerde Routes (UDR) met behulp van Azure CLI 2.0 Hallo maken

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Sjabloon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (klassieke implementatie)](virtual-network-create-udr-classic-ps.md)
> * [CLI (klassieke implementatie)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak 

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren: 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Hallo UDR voor Hallo front-end-subnet maken
toocreate hello routetabel en route die nodig zijn voor Hallo front-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.

1. Een routetabel voor Hallo front-end-subnet maken met de Hallo [az netwerk routetabel maken](/cli/azure/network/route-table#create) opdracht:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Uitvoer:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Maken van een route die alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) toohello verzendt **FW1** VM (192.168.0.4) met behulp van Hallo [az routetabel netwerkroute maken](/cli/azure/network/route-table/route#create) opdracht:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Uitvoer:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Parameters:

    * **--route tabelnaam**. Naam van de routetabel Hallo waar Hallo route wordt toegevoegd. In ons scenario *UDR FrontEnd*.
    * **--adresvoorvoegsel**. Het adresvoorvoegsel voor Hallo subnet waar pakketten zijn bestemd voor. In ons scenario *192.168.2.0/24*.
    * **--volgende hoptype**. Type object verkeer ontvangt. Mogelijke waarden zijn *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, of *geen*.
    * **--volgende hop-ip-adressen**. IP-adres voor de volgende hop. In ons scenario *192.168.0.4*.

3. Voer Hallo [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) opdracht tooassociate Hallo routetabel die eerder is gemaakt met de Hallo **FrontEnd** subnet:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Uitvoer:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Parameters:
    
    * **--vnet naam**. Naam van Hallo VNet waar Hallo subnet bevindt. In ons scenario *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Hallo UDR voor Hallo back-end subnet maken

toocreate hello routetabel en te routeren die nodig zijn voor Hallo back-end-subnet op basis van Hallo scenario hierboven voltooid Hallo stappen te volgen:

1. Voer Hallo opdracht toocreate na een routetabel voor Hallo back-end-subnet:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Voer hello na de opdracht tooassociate Hallo routetabel Hello **back-end** subnet:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Doorsturen via IP op FW1 inschakelen

doorsturen via IP in Hallo NIC die wordt gebruikt door tooenable **FW1**, volledige Hallo volgende stappen:

1. Voer Hallo [az netwerk nic weergeven](/cli/azure/network/nic#show) opdracht met een huidige van JMESPATH filter toodisplay hello **enable--doorsturen via ip** waarde voor **doorsturen via IP inschakelen**. Deze dient te worden ingesteld*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Uitvoer:

        false

2. Voer Hallo doorsturen via IP van opdracht tooenable te volgen:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Hallo uitvoer gestreamde toohello console controleren of alleen voor specifieke Hallo testen **enableIpForwarding** waarde:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Uitvoer:

        true

    Parameters:

    **---doorsturen via ip**: *true* of *false*.

