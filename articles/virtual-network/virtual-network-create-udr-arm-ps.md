---
title: aaaControl Routering en virtuele apparaten in Azure - PowerShell | Microsoft Docs
description: Meer informatie over hoe toocontrol Routering en virtuele apparaten met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="eda3f-103">Door de gebruiker gedefinieerde Routes (UDR) met behulp van PowerShell maken</span><span class="sxs-lookup"><span data-stu-id="eda3f-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eda3f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eda3f-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="eda3f-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eda3f-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="eda3f-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="eda3f-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="eda3f-107">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="eda3f-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="eda3f-108">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="eda3f-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="eda3f-109">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="eda3f-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="eda3f-110">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-resource-manager/resource-manager-deployment-model.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="eda3f-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="eda3f-111">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="eda3f-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="eda3f-112">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="eda3f-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="eda3f-113">U kunt ook [udr's maken in het klassieke implementatiemodel Hallo](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="eda3f-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="eda3f-114">Hallo voorbeeld PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="eda3f-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="eda3f-115">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal.</span><span class="sxs-lookup"><span data-stu-id="eda3f-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="eda3f-116">Hallo UDR voor Hallo front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="eda3f-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="eda3f-117">toocreate hello routetabel en route die nodig zijn voor de front-end-subnet Hallo gebaseerd op Hallo scenario hierboven voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="eda3f-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="eda3f-118">Maken van een route gebruikt toosend alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) gerouteerd toobe toohello **FW1** virtueel apparaat (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="eda3f-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="eda3f-119">Maken van een routetabel met de naam **UDR FrontEnd** in Hallo **westus** regio waarin Hallo route.</span><span class="sxs-lookup"><span data-stu-id="eda3f-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="eda3f-120">Maak een variabele met de Hallo VNet waar Hallo subnet is.</span><span class="sxs-lookup"><span data-stu-id="eda3f-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="eda3f-121">In ons scenario hello VNet heet **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="eda3f-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="eda3f-122">Routetabel koppelen Hallo bovenstaande toohello **FrontEnd** subnet.</span><span class="sxs-lookup"><span data-stu-id="eda3f-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="eda3f-123">Hallo-uitvoer voor bovenstaande Hallo-opdracht geeft Hallo-inhoud voor Hallo virtueel netwerk configuration-object bestaat alleen op Hallo-computer waarop u PowerShell worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eda3f-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="eda3f-124">U moet toorun hello **Set AzureVirtualNetwork** cmdlet toosave deze tooAzure instellingen.</span><span class="sxs-lookup"><span data-stu-id="eda3f-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="eda3f-125">Hallo nieuwe subnetconfiguratie op te slaan in Azure.</span><span class="sxs-lookup"><span data-stu-id="eda3f-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="eda3f-126">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="eda3f-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="eda3f-127">Hallo UDR voor Hallo back-end subnet maken</span><span class="sxs-lookup"><span data-stu-id="eda3f-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="eda3f-128">toocreate hello routetabel en route die nodig zijn voor Hallo back-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.</span><span class="sxs-lookup"><span data-stu-id="eda3f-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="eda3f-129">Maken van een route gebruikt toosend alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) gerouteerd toobe toohello **FW1** virtueel apparaat (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="eda3f-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="eda3f-130">Maken van een routetabel met de naam **UDR-back-end** in Hallo **uswest** regio Hallo route met die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eda3f-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="eda3f-131">Routetabel koppelen Hallo bovenstaande toohello **back-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="eda3f-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="eda3f-132">Hallo nieuwe subnetconfiguratie op te slaan in Azure.</span><span class="sxs-lookup"><span data-stu-id="eda3f-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="eda3f-133">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="eda3f-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="eda3f-134">Doorsturen via IP op FW1 inschakelen</span><span class="sxs-lookup"><span data-stu-id="eda3f-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="eda3f-135">doorsturen via IP in Hallo NIC die wordt gebruikt door tooenable **FW1**, volgt u onderstaande stappen voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="eda3f-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="eda3f-136">Maak een variabele die Hallo-instellingen voor Hallo NIC die wordt gebruikt door FW1 bevat.</span><span class="sxs-lookup"><span data-stu-id="eda3f-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="eda3f-137">In ons scenario hello NIC heet **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="eda3f-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="eda3f-138">Doorsturen via IP inschakelen en Hallo NIC-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="eda3f-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="eda3f-139">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="eda3f-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

