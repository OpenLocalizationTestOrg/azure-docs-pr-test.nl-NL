---
title: een virtueel netwerk - Azure PowerShell aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk met behulp van PowerShell.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a>Maak een virtueel netwerk met behulp van PowerShell

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek. Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel. Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.
 
Dit artikel wordt uitgelegd hoe toocreate een VNet via Hallo Resource Manager deployment model met behulp van PowerShell. Ook kunt u een VNet via Resource Manager, met andere hulpprogramma's maken of maak een VNet via de klassieke implementatiemodel Hallo door een andere optie kiezen in Hallo volgende lijst:

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

toocreate een virtueel netwerk met behulp van PowerShell, volledige Hallo volgende stappen:

1. Installeren en configureren van Azure PowerShell met de stappen te volgen Hallo in Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) artikel.

2. Maak indien nodig een resourcegroep aan, zoals hieronder wordt weergegeven. Voor dit scenario maakt u een resourcegroep met de naam *TestRG*. Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Verwachte uitvoer:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. Maak een nieuw VNet met de naam *TestVNet*:

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    Verwachte uitvoer:

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. Het virtuele netwerkobject Hallo opgeslagen in een variabele:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > U kunt stappen 3 en 4 combineren door het uitvoeren van `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.
   > 

5. Voeg een subnet toohello nieuwe VNet-variabele:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    Verwachte uitvoer:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. Herhaal stap 5 hierboven voor elk subnet gewenste toocreate. Hallo volgende opdracht maakt u Hallo *back-end* subnet voor Hallo scenario:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. Hoewel u subnetten aanmaakt, bestaan ze momenteel alleen in Hallo lokale variabele gebruikte tooretrieve hello VNet die u in stap 4 hierboven. toosave hello wijzigingen tooAzure, Hallo volgende opdracht uitvoeren:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    Verwachte uitvoer:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooconnect:

- Een virtueel netwerk van virtuele machine (VM) tooa door te lezen Hallo [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artikel. In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.
- virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artikel.
- Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit. Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-arm.md) artikelen.
