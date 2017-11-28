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
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="71090-103">Besturingselement Routering en gebruik virtuele apparaten (klassiek) met behulp van Hallo Azure CLI</span><span class="sxs-lookup"><span data-stu-id="71090-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="71090-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71090-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="71090-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="71090-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="71090-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="71090-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="71090-107">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="71090-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="71090-108">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="71090-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="71090-109">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="71090-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="71090-110">U kunt ook [beheren Routering en het gebruik van virtuele apparaten in de Resource Manager-implementatiemodel Hallo](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="71090-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="71090-111">Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="71090-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="71090-112">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, maakt u Hallo-omgeving wordt weergegeven in [een VNet maken (klassiek) met hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="71090-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="71090-113">Hallo UDR voor Hallo front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="71090-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="71090-114">toocreate hello routetabel en route die nodig zijn voor Hallo front-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.</span><span class="sxs-lookup"><span data-stu-id="71090-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="71090-115">Voer Hallo opdracht tooswitch tooclassic modus te volgen:</span><span class="sxs-lookup"><span data-stu-id="71090-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="71090-116">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71090-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="71090-117">Voer Hallo opdracht toocreate na een routetabel voor Hallo front-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="71090-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="71090-118">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71090-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="71090-119">Parameters:</span><span class="sxs-lookup"><span data-stu-id="71090-119">Parameters:</span></span>
   
   * <span data-ttu-id="71090-120">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="71090-120">**-l (or --location)**.</span></span> <span data-ttu-id="71090-121">Azure-regio waar hello nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71090-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="71090-122">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="71090-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="71090-123">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="71090-123">**-n (or --name)**.</span></span> <span data-ttu-id="71090-124">Naam voor Hallo nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="71090-124">Name for hello new NSG.</span></span> <span data-ttu-id="71090-125">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="71090-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="71090-126">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="71090-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="71090-127">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71090-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="71090-128">Parameters:</span><span class="sxs-lookup"><span data-stu-id="71090-128">Parameters:</span></span>
   
   * <span data-ttu-id="71090-129">**-r (of--route tabelnaam)**.</span><span class="sxs-lookup"><span data-stu-id="71090-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="71090-130">Naam van de routetabel Hallo waar Hallo route wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="71090-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="71090-131">In ons scenario *UDR FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="71090-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="71090-132">**-a (of --adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="71090-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="71090-133">Het adresvoorvoegsel voor Hallo subnet waar pakketten zijn bestemd voor.</span><span class="sxs-lookup"><span data-stu-id="71090-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="71090-134">In ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="71090-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="71090-135">**-t (of--volgende hoptype)**.</span><span class="sxs-lookup"><span data-stu-id="71090-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="71090-136">Type object verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="71090-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="71090-137">Mogelijke waarden zijn *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, of *geen*.</span><span class="sxs-lookup"><span data-stu-id="71090-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="71090-138">**-p (of--volgende hop-ip-adressen**).</span><span class="sxs-lookup"><span data-stu-id="71090-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="71090-139">IP-adres voor de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="71090-139">IP address for next hop.</span></span> <span data-ttu-id="71090-140">In ons scenario *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="71090-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="71090-141">Voer Hallo volgende opdracht tooassociate Hallo-routetabel is gemaakt met de Hallo **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="71090-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="71090-142">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71090-142">Output:</span></span>
   
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
   
    <span data-ttu-id="71090-143">Parameters:</span><span class="sxs-lookup"><span data-stu-id="71090-143">Parameters:</span></span>
   
   * <span data-ttu-id="71090-144">**-t (of--vnet naam)**.</span><span class="sxs-lookup"><span data-stu-id="71090-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="71090-145">Naam van Hallo VNet waar Hallo subnet bevindt.</span><span class="sxs-lookup"><span data-stu-id="71090-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="71090-146">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="71090-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="71090-147">**-n (of--subnet naam**.</span><span class="sxs-lookup"><span data-stu-id="71090-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="71090-148">Naam van de routetabel voor Hallo subnet hello wordt toegevoegd aan.</span><span class="sxs-lookup"><span data-stu-id="71090-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="71090-149">In ons scenario *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="71090-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="71090-150">Hallo UDR voor Hallo back-end subnet maken</span><span class="sxs-lookup"><span data-stu-id="71090-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="71090-151">toocreate hello routetabel en route die nodig zijn voor Hallo back-end-subnet op basis van Hallo scenario voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="71090-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="71090-152">Voer Hallo opdracht toocreate na een routetabel voor Hallo back-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="71090-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="71090-153">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="71090-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="71090-154">Voer hello na de opdracht tooassociate Hallo routetabel Hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="71090-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

