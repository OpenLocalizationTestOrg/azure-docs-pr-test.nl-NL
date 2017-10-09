---
title: aaaControl routering in een Azure Virtual Network - PowerShell - klassiek | Microsoft Docs
description: Meer informatie over hoe toocontrol routering in VNets met behulp van PowerShell | Klassieke
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
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="4cdcc-103">Beheren van Routering en het gebruik van virtuele apparaten (klassiek) met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cdcc-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cdcc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cdcc-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="4cdcc-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4cdcc-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="4cdcc-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="4cdcc-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="4cdcc-107">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4cdcc-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="4cdcc-108">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4cdcc-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="4cdcc-109">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="4cdcc-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4cdcc-110">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-resource-manager/resource-manager-deployment-model.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="4cdcc-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="4cdcc-111">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door een optie Hallo boven aan dit artikel te selecteren.</span><span class="sxs-lookup"><span data-stu-id="4cdcc-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="4cdcc-112">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4cdcc-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="4cdcc-113">Hallo voorbeeld Azure PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="4cdcc-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="4cdcc-114">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, maakt u Hallo-omgeving wordt weergegeven in [maken van een VNet (klassiek) met behulp van PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4cdcc-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="4cdcc-115">Hallo UDR voor Hallo front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="4cdcc-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="4cdcc-116">toocreate hello routetabel en route die nodig zijn voor Hallo front-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.</span><span class="sxs-lookup"><span data-stu-id="4cdcc-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="4cdcc-117">Voer Hallo opdracht toocreate na een routetabel voor Hallo front-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="4cdcc-118">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="4cdcc-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="4cdcc-119">Voer hello na de opdracht tooassociate Hallo routetabel Hello **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="4cdcc-120">Hallo UDR voor Hallo back-end subnet maken</span><span class="sxs-lookup"><span data-stu-id="4cdcc-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="4cdcc-121">toocreate hello routetabel en route die nodig zijn voor Hallo back subnet op basis van Hallo scenario beëindigen, voltooien Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="4cdcc-122">Voer Hallo opdracht toocreate na een routetabel voor Hallo back-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="4cdcc-123">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="4cdcc-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="4cdcc-124">Voer hello na de opdracht tooassociate Hallo routetabel Hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="4cdcc-125">Doorsturen via IP op Hallo FW1 VM inschakelen</span><span class="sxs-lookup"><span data-stu-id="4cdcc-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="4cdcc-126">tooenable doorsturen via IP in Hallo FW1 VM, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="4cdcc-127">Voer Hallo opdracht toocheck Hallo status van doorsturen via IP te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="4cdcc-128">Voer Hallo volgende opdracht doorsturen via IP voor Hallo tooenable *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="4cdcc-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
