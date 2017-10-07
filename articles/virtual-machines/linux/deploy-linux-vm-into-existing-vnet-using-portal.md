---
title: aaaDeploy virtuele Linux-machines in bestaande netwerk met Azure portal | Microsoft Docs
description: Linux-VM implementeren in een bestaand Azure virtueel netwerk met behulp van Hallo-portal.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="12ddb-103">Hoe toodeploy virtuele Linux-machine in Azure een bestaand virtueel netwerk met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="12ddb-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="12ddb-104">Dit artikel ziet u hoe toodeploy een virtuele machine (VM) in een bestaand virtueel netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="12ddb-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="12ddb-105">Azure activa zoals beveiligingsgroepen vnet's en het netwerk moeten statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="12ddb-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="12ddb-106">Zodra een VNet is geïmplementeerd, kan opnieuw door constante nieuwe distributies zonder een nadelige invloed toohello infrastructuur worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="12ddb-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="12ddb-107">Rekening houdt met een VNet dat deze een traditioneel netwerkswitch hardware - u hoeft dan niet een geheel nieuwe hardware overschakelen met elke implementatie tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="12ddb-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="12ddb-108">Met een juist geconfigureerde VNet, kunt u blijven toodeploy nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen gedurende de levensduur Hallo Hallo VNet vereist.</span><span class="sxs-lookup"><span data-stu-id="12ddb-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="12ddb-109">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="12ddb-109">Create hello resource group</span></span>

<span data-ttu-id="12ddb-110">Maak eerst een groep resource tooorganize alles wat die u in dit scenario maakt.</span><span class="sxs-lookup"><span data-stu-id="12ddb-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="12ddb-111">Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="12ddb-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="12ddb-113">Hallo VNet maken</span><span class="sxs-lookup"><span data-stu-id="12ddb-113">Create hello VNet</span></span>

<span data-ttu-id="12ddb-114">Bouw een VNet toolaunch Hallo vervolgens, virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="12ddb-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="12ddb-115">Hallo VNet bevat één subnet en is gekoppeld aan netwerkbeveiligingsgroep Hallo met dit subnet in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="12ddb-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="12ddb-117">Een VNic toohello subnet toevoegen</span><span class="sxs-lookup"><span data-stu-id="12ddb-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="12ddb-118">Virtueel-netwerkkaarten (VNics) zijn belangrijk als u verbinding ze toodifferent virtuele machines maken kunt.</span><span class="sxs-lookup"><span data-stu-id="12ddb-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="12ddb-119">Deze aanpak houdt Hallo VNic als statische resource Hallo VMs tijdelijke kan zijn.</span><span class="sxs-lookup"><span data-stu-id="12ddb-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="12ddb-120">Een VNic maken en deze koppelen aan Hallo subnet in de vorige stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12ddb-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="12ddb-122">Hallo netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="12ddb-122">Create hello network security group</span></span>

<span data-ttu-id="12ddb-123">Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="12ddb-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="12ddb-124">Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="12ddb-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="12ddb-126">Regel voor geven van een binnenkomende SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="12ddb-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="12ddb-127">Hallo VM moet toegang vanaf Hallo internet, zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 doorgegeven op Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12ddb-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="12ddb-129">Hallo NSG koppelen aan Hallo subnet</span><span class="sxs-lookup"><span data-stu-id="12ddb-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="12ddb-130">Hallo subnet koppelen Hallo netwerkbeveiligingsgroep met Hallo VNet en Hallo subnet gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12ddb-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="12ddb-131">Netwerkbeveiligingsgroepen kunnen worden gekoppeld aan een hele subnet of een afzonderlijke VNic.</span><span class="sxs-lookup"><span data-stu-id="12ddb-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="12ddb-132">Hallo Firewall voor het filteren van verkeer op Hallo subnetniveau, worden alle VNics en Hallo virtuele machines binnen Hallo subnet beveiligd door Hallo netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="12ddb-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="12ddb-133">Hallo is andere benadering Hallo network security groep wordt slechts een enkele VNic gekoppeld en slechts één virtuele machine te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="12ddb-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="12ddb-135">Hallo VM in Hallo VNet en NSG implementeren</span><span class="sxs-lookup"><span data-stu-id="12ddb-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="12ddb-136">Gebruik hello Azure-portal, is Hallo Linux VM geïmplementeerde toohello bestaande Azure-resourcegroep, VNet Subnet en VNic.</span><span class="sxs-lookup"><span data-stu-id="12ddb-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="12ddb-138">Met behulp van bestaande resources van Hallo portal toochoose vertelt u Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="12ddb-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="12ddb-139">Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="12ddb-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="12ddb-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12ddb-140">Next steps</span></span>

* [<span data-ttu-id="12ddb-141">Een Azure Resource Manager-sjabloon toocreate een specifieke implementatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="12ddb-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="12ddb-142">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="12ddb-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="12ddb-143">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="12ddb-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
