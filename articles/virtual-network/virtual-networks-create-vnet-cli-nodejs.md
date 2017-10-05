---
title: Een virtueel netwerk maken met de Azure CLI 1.0 | Microsoft Docs
description: Informatie over het maken van een virtueel netwerk met de Azure CLI 1.0 | Resource Manager.
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
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="bc0a8-103">Een virtueel netwerk maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bc0a8-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="bc0a8-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="bc0a8-105">Microsoft raadt aan resources te maken via het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="bc0a8-106">Lees het artikel [Azure-implementatiemodellen begrijpen](../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie over de verschillen tussen de twee modellen.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bc0a8-107">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="bc0a8-107">CLI versions to complete the task</span></span>
<span data-ttu-id="bc0a8-108">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="bc0a8-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="bc0a8-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="bc0a8-110">[Azure CLI 1.0](#create-a-virtual-network) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="bc0a8-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="bc0a8-111">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="bc0a8-111">Create a virtual network</span></span>

<span data-ttu-id="bc0a8-112">Voor het maken van een virtueel netwerk met de Azure CLI, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="bc0a8-113">Installeren en configureren van de Azure CLI met de stappen in de [installeren en configureren van de Azure CLI](../cli-install-nodejs.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="bc0a8-114">Een VNet en een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="bc0a8-115">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="bc0a8-116">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-116">Parameters used:</span></span>

   * <span data-ttu-id="bc0a8-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-117">**--vnet**.</span></span> <span data-ttu-id="bc0a8-118">Naam van de VNet die moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-118">Name of the VNet to be created.</span></span> <span data-ttu-id="bc0a8-119">In ons scenario *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="bc0a8-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="bc0a8-120">**-e (of--adresruimte)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="bc0a8-121">VNet-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-121">VNet address space.</span></span> <span data-ttu-id="bc0a8-122">In ons scenario *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="bc0a8-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="bc0a8-123">**-i (of de cidr-)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="bc0a8-124">Het netwerkmasker in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-124">Network mask in CIDR format.</span></span> <span data-ttu-id="bc0a8-125">In ons scenario *16*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="bc0a8-126">**-n (of--subnet naam**).</span><span class="sxs-lookup"><span data-stu-id="bc0a8-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="bc0a8-127">Naam van het eerste subnet.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-127">Name of the first subnet.</span></span> <span data-ttu-id="bc0a8-128">In ons scenario *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="bc0a8-129">**-p (of--begin-ip-subnet)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="bc0a8-130">IP-adres voor het subnet of subnetadresruimte wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="bc0a8-131">In ons scenario *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="bc0a8-132">**-r (of--subnet cidr)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="bc0a8-133">Het netwerkmasker in CIDR-indeling voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="bc0a8-134">In ons scenario *24*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="bc0a8-135">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-135">**-l (or --location)**.</span></span> <span data-ttu-id="bc0a8-136">Azure-regio waar de VNet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="bc0a8-137">In ons scenario *VS-midden*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="bc0a8-138">Een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="bc0a8-139">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="bc0a8-140">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-140">Parameters used:</span></span>

   * <span data-ttu-id="bc0a8-141">**-t (of--vnet naam**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="bc0a8-142">Naam van de VNet waar het subnet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="bc0a8-143">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="bc0a8-144">**-n (of --name)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-144">**-n (or --name)**.</span></span> <span data-ttu-id="bc0a8-145">Naam van het nieuwe subnet.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-145">Name of the new subnet.</span></span> <span data-ttu-id="bc0a8-146">In ons scenario *back-end*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="bc0a8-147">**-a (of --adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="bc0a8-148">Subnet CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-148">Subnet CIDR block.</span></span> <span data-ttu-id="bc0a8-149">Vier in ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="bc0a8-150">De eigenschappen van de nieuwe VNet weergeven:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="bc0a8-151">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
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

## <a name="next-steps"></a><span data-ttu-id="bc0a8-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc0a8-152">Next steps</span></span>

<span data-ttu-id="bc0a8-153">Leer hoe u de volgende verbindingen maakt:</span><span class="sxs-lookup"><span data-stu-id="bc0a8-153">Learn how to connect:</span></span>

- <span data-ttu-id="bc0a8-154">Een virtuele machine (VM) met een virtueel netwerk door het lezen van de [maken van een Linux-VM](../virtual-machines/linux/quick-create-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="bc0a8-155">In plaats van een VNet en subnet te maken via de stappen die in de artikelen worden beschreven, kunt u ook een bestaand VNet en subnet selecteren waarmee u een VM wilt verbinden.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="bc0a8-156">Verbinding van het virtuele netwerk met andere virtuele netwerken: lees het artikel [VNets verbinden](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc0a8-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="bc0a8-157">Verbinding van het virtuele netwerk met een on-premises netwerk via een site-naar-site virtueel particulier netwerk (VPN) of een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="bc0a8-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="bc0a8-158">Meer informatie over hoe door het lezen van de [verbinding van een VNet met een on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [een VNet koppelen aan een ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bc0a8-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>