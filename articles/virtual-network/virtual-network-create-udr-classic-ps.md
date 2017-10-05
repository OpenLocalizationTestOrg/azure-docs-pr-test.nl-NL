---
title: Routering in een Azure Virtual Network - PowerShell - klassiek beheren | Microsoft Docs
description: Meer informatie over het beheren van routering in VNets met behulp van PowerShell | Klassieke
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: e9564d223cb85529f1fa97bc398d35c6debcedae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="f8172-103">Beheren van Routering en het gebruik van virtuele apparaten (klassiek) met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8172-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8172-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8172-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="f8172-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f8172-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="f8172-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="f8172-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="f8172-107">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="f8172-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="f8172-108">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="f8172-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f8172-109">Voordat u met Azure-resources gaat werken, is het belangrijk om te weten dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="f8172-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f8172-110">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-resource-manager/resource-manager-deployment-model.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="f8172-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="f8172-111">U kunt de documentatie voor verschillende hulpprogramma's bekijken door een optie boven aan dit artikel te selecteren.</span><span class="sxs-lookup"><span data-stu-id="f8172-111">You can view the documentation for different tools by selecting an option at the top of this article.</span></span> <span data-ttu-id="f8172-112">Dit artikel is van toepassing op het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f8172-112">This article covers the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="f8172-113">Het voorbeeld Azure PowerShell onderstaande opdrachten een eenvoudige omgeving al gemaakt verwacht op basis van het bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="f8172-113">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="f8172-114">Als u uitvoeren van de opdrachten wilt zoals ze worden weergegeven in dit document, maakt u de omgeving wordt weergegeven in [maken van een VNet (klassiek) met behulp van PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f8172-114">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="f8172-115">De UDR voor de front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="f8172-115">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="f8172-116">Volg de onderstaande stappen voor het maken van de routetabel en de route die nodig zijn voor de front-end-subnet op basis van de bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="f8172-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="f8172-117">Voer de volgende opdracht voor het maken van een routetabel voor de front-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="f8172-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="f8172-118">Voer de volgende opdracht voor het maken van een route in de routetabel alle verkeer dat is bestemd voor het subnet voor back-end (192.168.2.0/24) te verzenden naar de **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f8172-118">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="f8172-119">Voer de volgende opdracht om te koppelen van de routetabel met de **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="f8172-119">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="f8172-120">De UDR voor de back-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="f8172-120">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="f8172-121">Voor het maken van de routetabel en de route die nodig zijn voor de back-end-subnet op basis van het scenario, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f8172-121">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="f8172-122">Voer de volgende opdracht voor het maken van een routetabel voor de back-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="f8172-122">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="f8172-123">Voer de volgende opdracht voor het maken van een route in de routetabel alle verkeer dat is bestemd voor het front-end-subnet (192.168.1.0/24) te verzenden naar de **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f8172-123">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="f8172-124">Voer de volgende opdracht om te koppelen van de routetabel met de **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="f8172-124">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="f8172-125">Doorsturen via IP op de VM FW1 inschakelen</span><span class="sxs-lookup"><span data-stu-id="f8172-125">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="f8172-126">Om in te schakelen IP doorsturen in de VM FW1, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f8172-126">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="f8172-127">Voer de volgende opdracht om de status van doorsturen via IP te controleren:</span><span class="sxs-lookup"><span data-stu-id="f8172-127">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="f8172-128">Voer de volgende opdracht om in te schakelen doorsturen via IP voor de *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="f8172-128">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
