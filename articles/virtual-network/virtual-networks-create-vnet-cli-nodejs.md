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
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="56806-103">Een virtueel netwerk maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56806-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="56806-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="56806-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="56806-105">Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="56806-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="56806-106">Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="56806-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="56806-107">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="56806-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="56806-108">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="56806-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="56806-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="56806-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="56806-110">[Azure CLI 1.0](#create-a-virtual-network) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="56806-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="56806-111">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="56806-111">Create a virtual network</span></span>

<span data-ttu-id="56806-112">een virtueel netwerk met toocreate hello Azure CLI, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="56806-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="56806-113">Installeren en configureren van Azure CLI door de volgende Hallo stappen Hallo in Hallo [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="56806-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="56806-114">Een VNet en een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="56806-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="56806-115">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="56806-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="56806-116">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="56806-116">Parameters used:</span></span>

   * <span data-ttu-id="56806-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="56806-117">**--vnet**.</span></span> <span data-ttu-id="56806-118">Naam van Hallo VNet toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="56806-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="56806-119">In ons scenario *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="56806-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="56806-120">**-e (of--adresruimte)**.</span><span class="sxs-lookup"><span data-stu-id="56806-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="56806-121">VNet-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="56806-121">VNet address space.</span></span> <span data-ttu-id="56806-122">In ons scenario *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="56806-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="56806-123">**-i (of de cidr-)**.</span><span class="sxs-lookup"><span data-stu-id="56806-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="56806-124">Het netwerkmasker in CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="56806-124">Network mask in CIDR format.</span></span> <span data-ttu-id="56806-125">In ons scenario *16*.</span><span class="sxs-lookup"><span data-stu-id="56806-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="56806-126">**-n (of--subnet naam**).</span><span class="sxs-lookup"><span data-stu-id="56806-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="56806-127">Naam van het eerste subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="56806-127">Name of hello first subnet.</span></span> <span data-ttu-id="56806-128">In ons scenario *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="56806-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="56806-129">**-p (of--begin-ip-subnet)**.</span><span class="sxs-lookup"><span data-stu-id="56806-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="56806-130">IP-adres voor het subnet of subnetadresruimte wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="56806-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="56806-131">In ons scenario *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="56806-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="56806-132">**-r (of--subnet cidr)**.</span><span class="sxs-lookup"><span data-stu-id="56806-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="56806-133">Het netwerkmasker in CIDR-indeling voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="56806-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="56806-134">In ons scenario *24*.</span><span class="sxs-lookup"><span data-stu-id="56806-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="56806-135">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="56806-135">**-l (or --location)**.</span></span> <span data-ttu-id="56806-136">Azure-regio waar Hallo VNet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="56806-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="56806-137">In ons scenario *VS-midden*.</span><span class="sxs-lookup"><span data-stu-id="56806-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="56806-138">Een subnet maken:</span><span class="sxs-lookup"><span data-stu-id="56806-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="56806-139">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="56806-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="56806-140">Gebruikte parameters:</span><span class="sxs-lookup"><span data-stu-id="56806-140">Parameters used:</span></span>

   * <span data-ttu-id="56806-141">**-t (of--vnet naam**.</span><span class="sxs-lookup"><span data-stu-id="56806-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="56806-142">Naam van Hallo VNet waar Hallo subnet wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="56806-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="56806-143">In ons scenario *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="56806-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="56806-144">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="56806-144">**-n (or --name)**.</span></span> <span data-ttu-id="56806-145">Naam van nieuw subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="56806-145">Name of hello new subnet.</span></span> <span data-ttu-id="56806-146">In ons scenario *back-end*.</span><span class="sxs-lookup"><span data-stu-id="56806-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="56806-147">**-a (of --adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="56806-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="56806-148">Subnet CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="56806-148">Subnet CIDR block.</span></span> <span data-ttu-id="56806-149">Vier in ons scenario *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="56806-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="56806-150">tooview hello eigenschappen van nieuwe VNet Hallo:</span><span class="sxs-lookup"><span data-stu-id="56806-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="56806-151">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="56806-151">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="56806-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56806-152">Next steps</span></span>

<span data-ttu-id="56806-153">Meer informatie over hoe tooconnect:</span><span class="sxs-lookup"><span data-stu-id="56806-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="56806-154">Een virtueel netwerk van virtuele machine (VM) tooa door te lezen Hallo [maken van een Linux-VM](../virtual-machines/linux/quick-create-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="56806-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="56806-155">In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.</span><span class="sxs-lookup"><span data-stu-id="56806-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="56806-156">virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="56806-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="56806-157">Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="56806-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="56806-158">Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="56806-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
