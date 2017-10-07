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
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="3d410-103">Maak een virtueel netwerk met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d410-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="3d410-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="3d410-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3d410-105">Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3d410-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="3d410-106">Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3d410-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="3d410-107">Dit artikel wordt uitgelegd hoe toocreate een VNet via Hallo Resource Manager deployment model met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d410-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="3d410-108">Ook kunt u een VNet via Resource Manager, met andere hulpprogramma's maken of maak een VNet via de klassieke implementatiemodel Hallo door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="3d410-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d410-109">Portal</span><span class="sxs-lookup"><span data-stu-id="3d410-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="3d410-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d410-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="3d410-111">CLI</span><span class="sxs-lookup"><span data-stu-id="3d410-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="3d410-112">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="3d410-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="3d410-113">Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="3d410-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="3d410-114">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="3d410-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="3d410-115">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="3d410-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="3d410-116">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="3d410-116">Create a virtual network</span></span>

<span data-ttu-id="3d410-117">toocreate een virtueel netwerk met behulp van PowerShell, volledige Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="3d410-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="3d410-118">Installeren en configureren van Azure PowerShell met de stappen te volgen Hallo in Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="3d410-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="3d410-119">Maak indien nodig een resourcegroep aan, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3d410-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="3d410-120">Voor dit scenario maakt u een resourcegroep met de naam *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="3d410-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="3d410-121">Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="3d410-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="3d410-122">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3d410-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="3d410-123">Maak een nieuw VNet met de naam *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="3d410-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="3d410-124">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3d410-124">Expected output:</span></span>

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
4. <span data-ttu-id="3d410-125">Het virtuele netwerkobject Hallo opgeslagen in een variabele:</span><span class="sxs-lookup"><span data-stu-id="3d410-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="3d410-126">U kunt stappen 3 en 4 combineren door het uitvoeren van `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="3d410-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="3d410-127">Voeg een subnet toohello nieuwe VNet-variabele:</span><span class="sxs-lookup"><span data-stu-id="3d410-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="3d410-128">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3d410-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="3d410-129">Herhaal stap 5 hierboven voor elk subnet gewenste toocreate.</span><span class="sxs-lookup"><span data-stu-id="3d410-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="3d410-130">Hallo volgende opdracht maakt u Hallo *back-end* subnet voor Hallo scenario:</span><span class="sxs-lookup"><span data-stu-id="3d410-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="3d410-131">Hoewel u subnetten aanmaakt, bestaan ze momenteel alleen in Hallo lokale variabele gebruikte tooretrieve hello VNet die u in stap 4 hierboven.</span><span class="sxs-lookup"><span data-stu-id="3d410-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="3d410-132">toosave hello wijzigingen tooAzure, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3d410-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="3d410-133">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3d410-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="3d410-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d410-134">Next steps</span></span>

<span data-ttu-id="3d410-135">Meer informatie over hoe tooconnect:</span><span class="sxs-lookup"><span data-stu-id="3d410-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="3d410-136">Een virtueel netwerk van virtuele machine (VM) tooa door te lezen Hallo [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3d410-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="3d410-137">In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.</span><span class="sxs-lookup"><span data-stu-id="3d410-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="3d410-138">virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3d410-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="3d410-139">Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="3d410-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="3d410-140">Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-arm.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="3d410-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
