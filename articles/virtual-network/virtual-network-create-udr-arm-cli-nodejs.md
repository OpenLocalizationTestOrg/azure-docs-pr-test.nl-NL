---
title: aaaControl Routering en virtuele apparaten via Azure CLI 1.0 Hallo | Microsoft Docs
description: Meer informatie over hoe toocontrol Routering en virtuele apparaten via Azure CLI 1.0 Hallo.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="05864-103">Door de gebruiker gedefinieerde Routes (UDR) met behulp van Azure CLI 1.0 Hallo maken</span><span class="sxs-lookup"><span data-stu-id="05864-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05864-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05864-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="05864-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05864-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="05864-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="05864-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="05864-107">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="05864-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="05864-108">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="05864-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="05864-109">Maak aangepaste Routering en virtuele apparaten met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="05864-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="05864-110">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="05864-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="05864-111">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="05864-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="05864-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="05864-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="05864-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="05864-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="05864-114">Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="05864-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="05864-115">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal.</span><span class="sxs-lookup"><span data-stu-id="05864-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="05864-116">Hallo UDR voor Hallo front-end-subnet maken</span><span class="sxs-lookup"><span data-stu-id="05864-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="05864-117">toocreate hello routetabel en route die nodig zijn voor Hallo front-end-subnet op basis van Hallo scenario bovenstaande stappen Hallo hieronder.</span><span class="sxs-lookup"><span data-stu-id="05864-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="05864-118">Voer Hallo opdracht toocreate na een routetabel voor Hallo front-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="05864-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="05864-119">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="05864-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="05864-120">Parameters:</span><span class="sxs-lookup"><span data-stu-id="05864-120">Parameters:</span></span>
   
   * <span data-ttu-id="05864-121">**-g (of --resourcegroep)**.</span><span class="sxs-lookup"><span data-stu-id="05864-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="05864-122">Naam van resourcegroep Hallo waar Hallo UDR wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="05864-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="05864-123">In ons scenario *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="05864-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="05864-124">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="05864-124">**-l (or --location)**.</span></span> <span data-ttu-id="05864-125">Azure-regio waar hello nieuwe UDR wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="05864-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="05864-126">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="05864-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="05864-127">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="05864-127">**-n (or --name)**.</span></span> <span data-ttu-id="05864-128">Naam voor Hallo nieuwe UDR.</span><span class="sxs-lookup"><span data-stu-id="05864-128">Name for hello new UDR.</span></span> <span data-ttu-id="05864-129">In ons scenario *UDR FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="05864-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="05864-130">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello back-end-subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="05864-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="05864-131">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="05864-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="05864-132">Parameters:</span><span class="sxs-lookup"><span data-stu-id="05864-132">Parameters:</span></span>
   
   * <span data-ttu-id="05864-133">**-r (of--route tabelnaam)**.</span><span class="sxs-lookup"><span data-stu-id="05864-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="05864-134">Naam van de routetabel Hallo waar Hallo route wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="05864-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="05864-135">In ons scenario *UDR FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="05864-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="05864-136">**-a (of --adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="05864-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="05864-137">Het adresvoorvoegsel voor Hallo subnet waar pakketten zijn bestemd voor.</span><span class="sxs-lookup"><span data-stu-id="05864-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="05864-138">In ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="05864-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="05864-139">**-y (of--volgende hoptype)**.</span><span class="sxs-lookup"><span data-stu-id="05864-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="05864-140">Type object verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="05864-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="05864-141">Mogelijke waarden zijn *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, of *geen*.</span><span class="sxs-lookup"><span data-stu-id="05864-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="05864-142">**-p (of--volgende hop-ip-adressen**).</span><span class="sxs-lookup"><span data-stu-id="05864-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="05864-143">IP-adres voor de volgende hop.</span><span class="sxs-lookup"><span data-stu-id="05864-143">IP address for next hop.</span></span> <span data-ttu-id="05864-144">In ons scenario *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="05864-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="05864-145">Voer Hallo volgende opdracht tooassociate Hallo-routetabel die eerder is gemaakt met de Hallo **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="05864-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="05864-146">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="05864-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="05864-147">Parameters:</span><span class="sxs-lookup"><span data-stu-id="05864-147">Parameters:</span></span>
   
   * <span data-ttu-id="05864-148">**-e (of--vnet naam)**.</span><span class="sxs-lookup"><span data-stu-id="05864-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="05864-149">Naam van Hallo VNet waar Hallo subnet bevindt.</span><span class="sxs-lookup"><span data-stu-id="05864-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="05864-150">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="05864-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="05864-151">Hallo UDR voor Hallo back-end subnet maken</span><span class="sxs-lookup"><span data-stu-id="05864-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="05864-152">toocreate hello routetabel en te routeren die nodig zijn voor Hallo back-end-subnet op basis van Hallo scenario hierboven voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="05864-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="05864-153">Voer Hallo opdracht toocreate na een routetabel voor Hallo back-end-subnet:</span><span class="sxs-lookup"><span data-stu-id="05864-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="05864-154">Uitvoeren na de opdracht toocreate een route in Hallo route tabel toosend Hallo alle verkeer dat is bestemd toohello front-end-subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="05864-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="05864-155">Voer hello na de opdracht tooassociate Hallo routetabel Hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="05864-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="05864-156">Doorsturen via IP op FW1 inschakelen</span><span class="sxs-lookup"><span data-stu-id="05864-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="05864-157">doorsturen via IP in Hallo NIC die wordt gebruikt door tooenable **FW1**, volledige Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="05864-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="05864-158">Voer Hallo-opdracht weergegeven en u ziet Hallo-waarde voor **doorsturen via IP inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="05864-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="05864-159">Deze dient te worden ingesteld*false*.</span><span class="sxs-lookup"><span data-stu-id="05864-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="05864-160">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="05864-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="05864-161">Voer Hallo doorsturen via IP van opdracht tooenable te volgen:</span><span class="sxs-lookup"><span data-stu-id="05864-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="05864-162">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="05864-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="05864-163">Parameters:</span><span class="sxs-lookup"><span data-stu-id="05864-163">Parameters:</span></span>
   
   * <span data-ttu-id="05864-164">**-f (of--enable--doorsturen via ip)**.</span><span class="sxs-lookup"><span data-stu-id="05864-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="05864-165">*de waarde True* of *false*.</span><span class="sxs-lookup"><span data-stu-id="05864-165">*true* or *false*.</span></span>

