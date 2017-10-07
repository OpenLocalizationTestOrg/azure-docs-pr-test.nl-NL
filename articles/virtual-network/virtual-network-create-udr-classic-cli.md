---
title: aaaControl routering in een klassiek virtueel netwerk van Azure - CLI - | Microsoft Docs
description: Meer informatie over hoe toocontrol routering in VNets met behulp van Azure CLI Hallo Hallo klassieke implementatiemodel
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Besturingselement Routering en gebruik virtuele apparaten (klassiek) met behulp van Hallo Azure CLI

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Sjabloon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (klassiek)](virtual-network-create-udr-classic-ps.md)
> * [CLI (klassiek)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [beheren Routering en het gebruik van virtuele apparaten in de Resource Manager-implementatiemodel Hallo](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, maakt u Hallo-omgeving wordt weergegeven in [een VNet maken (klassiek) met hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Hallo UDR voor Hallo front-end-subnet maken
toocreate hello routetabel en route die nodig zijn voor Hallo front-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.

1. Voer Hallo opdracht tooswitch tooclassic modus te volgen:

    ```azurecli
    azure config mode asm
    ```

    Uitvoer:

        info:    New mode is asm

2. Voer Hallo opdracht toocreate na een routetabel voor Hallo front-end-subnet:

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Uitvoer:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Parameters:
   
   * **-l (of --locatie)**. Azure-regio waar hello nieuwe NSG wordt gemaakt. In ons scenario *westus*.
   * **-n (of --naam)**. Naam voor Hallo nieuwe NSG. In ons scenario *NSG-FrontEnd*.
3. Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Uitvoer:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Parameters:
   
   * **-r (of--route tabelnaam)**. Naam van de routetabel Hallo waar Hallo route wordt toegevoegd. In ons scenario *UDR FrontEnd*.
   * **-a (of --adresvoorvoegsel)**. Het adresvoorvoegsel voor Hallo subnet waar pakketten zijn bestemd voor. In ons scenario *192.168.2.0/24*.
   * **-t (of--volgende hoptype)**. Type object verkeer ontvangt. Mogelijke waarden zijn *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, of *geen*.
   * **-p (of--volgende hop-ip-adressen**). IP-adres voor de volgende hop. In ons scenario *192.168.0.4*.
4. Voer Hallo volgende opdracht tooassociate Hallo-routetabel is gemaakt met de Hallo **FrontEnd** subnet:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Uitvoer:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Parameters:
   
   * **-t (of--vnet naam)**. Naam van Hallo VNet waar Hallo subnet bevindt. In ons scenario *TestVNet*.
   * **-n (of--subnet naam**. Naam van de routetabel voor Hallo subnet hello wordt toegevoegd aan. In ons scenario *FrontEnd*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Hallo UDR voor Hallo back-end subnet maken
toocreate hello routetabel en route die nodig zijn voor Hallo back-end-subnet op basis van Hallo scenario voltooid Hallo stappen te volgen:

1. Voer Hallo opdracht toocreate na een routetabel voor Hallo back-end-subnet:

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Voer hello na de opdracht tooassociate Hallo routetabel Hello **back-end** subnet:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

