---
title: een virtueel netwerk - Azure CLI 2.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk met Azure CLI 2.0 Hallo.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Een virtueel netwerk maken met hello Azure CLI 2.0

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek. Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel. Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – onze CLI voor Hallo klassieke en resource management implementatiemodellen
- [Azure CLI 2.0](#create-a-virtual-network) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)'
 
    Ook kunt u een VNet via Resource Manager, met andere hulpprogramma's maken of maak een VNet via de klassieke implementatiemodel Hallo door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Sjabloon](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (klassiek)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (klassiek)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (klassiek)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Een virtueel netwerk maken

een virtueel netwerk met toocreate hello Azure CLI 2.0, volledige Hallo stappen te volgen:

1. Installeer en configureer Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).

2. Een resourcegroep maken voor uw VNet met Hallo [az groep maken](/cli/azure/group#create) opdracht Hello `--name` en `--location` argumenten:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Een VNet en een subnet maken:

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Verwachte uitvoer:
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Gebruikte parameters:

    - `--name TestVNet`: De naam van Hallo VNet toobe gemaakt.
    - `--resource-group TestRG`: # Hallo Resourcegroepnaam die Hallo resource bepaalt. 
    - `--location centralus`: locatie naar welke toodeploy Hallo.
    - `--address-prefix 192.168.0.0/16`: Hallo adresvoorvoegsel en blokkeren.  
    - `--subnet-name FrontEnd`: Hallo-naam van het Hallo-subnet.
    - `--subnet-prefix 192.168.1.0/24`: Hallo adresvoorvoegsel en blokkeren.

    toolist hello basisinformatie toouse in Hallo naast uitvoert, en u kunt een query Hallo VNet met behulp van een [queryfilter](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Hallo na uitvoer, die wordt gegenereerd:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Een subnet maken:

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Verwachte uitvoer:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Gebruikte parameters:

    - `--address-prefix 192.168.2.0/24`: Subnet CIDR-blok.
    - `--name BackEnd`: De naam van nieuw subnet Hallo.
    - `--resource-group TestRG`: Hallo resourcegroep.
    - `--vnet-name TestVNet`: naam Hallo Hallo die eigenaar is van VNet.

5. Query Hallo eigenschappen van nieuwe VNet Hallo:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Verwachte uitvoer:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Eigenschappen van de query Hallo van Hallo subnetten:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Verwachte uitvoer:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooconnect:

- Een virtueel netwerk van virtuele machine (VM) tooa door te lezen Hallo [maken van een Linux-VM](../virtual-machines/linux/quick-create-cli.md) artikel. In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.
- virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artikel.
- Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit. Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
