---
title: een virtueel netwerk met aaaCreate hello Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk met Azure CLI 1.0 Hallo | Resource Manager.
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Een virtueel netwerk maken met hello Azure CLI

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek. Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel. Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel
- [Azure CLI 1.0](#create-a-virtual-network) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Een virtueel netwerk maken

een virtueel netwerk met toocreate hello Azure CLI, volledige Hallo stappen te volgen:

1. Installeren en configureren van Azure CLI door de volgende Hallo stappen Hallo in Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) artikel.

2. Een VNet en een subnet maken:

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Verwachte uitvoer:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Gebruikte parameters:

   * **--vnet**. Naam van Hallo VNet toobe gemaakt. In ons scenario *TestVNet*
   * **-e (of--adresruimte)**. VNet-adresruimte. In ons scenario *192.168.0.0*
   * **-i (of de cidr-)**. Het netwerkmasker in CIDR-notatie. In ons scenario *16*.
   * **-n (of--subnet naam**). Naam van het eerste subnet Hallo. In ons scenario *FrontEnd*.
   * **-p (of--begin-ip-subnet)**. IP-adres voor het subnet of subnetadresruimte wordt gestart. In ons scenario *192.168.1.0*.
   * **-r (of--subnet cidr)**. Het netwerkmasker in CIDR-indeling voor het subnet. In ons scenario *24*.
   * **-l (of --locatie)**. Azure-regio waar Hallo VNet wordt gemaakt. In ons scenario *VS-midden*.

3. Een subnet maken:

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Verwachte uitvoer:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Gebruikte parameters:

   * **-t (of--vnet naam**. Naam van Hallo VNet waar Hallo subnet wordt gemaakt. In ons scenario *TestVNet*.
   * **-n (of --naam)**. Naam van nieuw subnet Hallo. In ons scenario *back-end*.
   * **-a (of --adresvoorvoegsel)**. Subnet CIDR-blok. Vier in ons scenario *192.168.2.0/24*.
   
4. tooview hello eigenschappen van nieuwe VNet Hallo:

    ```azurecli
    azure network vnet show
    ```
   
    Verwachte uitvoer:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooconnect:

- Een virtueel netwerk van virtuele machine (VM) tooa door te lezen Hallo [maken van een Linux-VM](../virtual-machines/linux/quick-create-cli.md) artikel. In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.
- virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artikel.
- Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit. Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
