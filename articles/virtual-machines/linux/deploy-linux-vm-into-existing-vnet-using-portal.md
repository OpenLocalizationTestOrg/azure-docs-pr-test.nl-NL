---
title: Implementeren van virtuele Linux-machines in bestaande netwerk met Azure portal | Microsoft Docs
description: Implementeer een Linux-VM naar een bestaande Azure-netwerk met behulp van de portal.
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
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a><span data-ttu-id="3e0a1-103">Het implementeren van een virtuele Linux-machine in Azure een bestaand virtueel netwerk met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3e0a1-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure portal</span></span>

<span data-ttu-id="3e0a1-104">In dit artikel laat zien hoe een virtuele machine (VM) implementeren in een bestaand virtueel netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="3e0a1-104">This article shows you how to deploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="3e0a1-105">Azure activa zoals beveiligingsgroepen vnet's en het netwerk moeten statisch en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="3e0a1-106">Zodra een VNet is geïmplementeerd, kan dit opnieuw gebruikt door constante nieuwe distributies zonder een ongewenst is van invloed op de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="3e0a1-107">Rekening houdt met een VNet dat deze een traditioneel netwerkswitch hardware - u niet moet een geheel nieuwe hardwareswitch configureren met elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-107">Thinking about a VNet as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="3e0a1-108">U kunt blijven implementeren nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen die zijn vereist tijdens de levensduur van het VNet met een juist geconfigureerde VNet.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-108">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="3e0a1-109">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="3e0a1-109">Create the resource group</span></span>

<span data-ttu-id="3e0a1-110">Maak eerst een resourcegroep te organiseren alles wat die u in dit scenario maakt.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-110">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="3e0a1-111">Zie voor meer informatie over Azure-resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3e0a1-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a><span data-ttu-id="3e0a1-113">Het VNet maken</span><span class="sxs-lookup"><span data-stu-id="3e0a1-113">Create the VNet</span></span>

<span data-ttu-id="3e0a1-114">Vervolgens start de virtuele machines in een VNet maken.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-114">Next, build a VNet to launch the VMs into.</span></span> <span data-ttu-id="3e0a1-115">Het VNet bevat één subnet en is gekoppeld aan de netwerkbeveiligingsgroep met dit subnet in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-115">The VNet contains one subnet and is associated with the network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="3e0a1-117">Een VNic toevoegen aan het subnet</span><span class="sxs-lookup"><span data-stu-id="3e0a1-117">Add a VNic to the subnet</span></span>

<span data-ttu-id="3e0a1-118">Virtueel-netwerkkaarten (VNics) zijn belangrijk omdat u ze met andere virtuele machines verbinden kunt.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-118">Virtual network cards (VNics) are important as you can connect them to different VMs.</span></span> <span data-ttu-id="3e0a1-119">Deze aanpak houdt de VNic als statische resource terwijl de virtuele machines kunnen tijdelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-119">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="3e0a1-120">Een VNic maken en deze koppelen aan het subnet in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-120">Create a VNic and associate it with the subnet created in the previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a><span data-ttu-id="3e0a1-122">De netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="3e0a1-122">Create the network security group</span></span>

<span data-ttu-id="3e0a1-123">Beveiligingsgroepen voor Azure-netwerk zijn equivalent aan een firewall op de netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-123">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="3e0a1-124">Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3e0a1-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="3e0a1-126">Regel voor geven van een binnenkomende SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e0a1-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="3e0a1-127">De virtuele machine moet toegang via het internet, zodat een regel binnenkomende poort 22-verkeer via het netwerk worden doorgegeven aan poort 22 op de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-127">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a><span data-ttu-id="3e0a1-129">Het NSG koppelen aan het subnet</span><span class="sxs-lookup"><span data-stu-id="3e0a1-129">Associate the NSG with the subnet</span></span>

<span data-ttu-id="3e0a1-130">Met het VNet en het subnet dat is gemaakt door de netwerkbeveiligingsgroep te koppelen aan het subnet.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-130">With the VNet and the subnet created, associate the network security group with the subnet.</span></span> <span data-ttu-id="3e0a1-131">Netwerkbeveiligingsgroepen kunnen worden gekoppeld aan een hele subnet of een afzonderlijke VNic.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="3e0a1-132">Alle VNics en de virtuele machines binnen het subnet met de firewall verkeer op subnetniveau filteren, worden beveiligd door de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-132">With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the network security group.</span></span> <span data-ttu-id="3e0a1-133">De andere benadering is de netwerkbeveiligingsgroep kan met slechts een enkele VNic en beveiligende slechts één virtuele machine worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-133">The other approach is the network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="3e0a1-135">Implementeer de virtuele machine in het VNet en het NSG</span><span class="sxs-lookup"><span data-stu-id="3e0a1-135">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="3e0a1-136">Met de Azure portal, wordt de Linux-VM geïmplementeerd op de bestaande Azure-resourcegroep, VNet, Subnet en VNic.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-136">Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="3e0a1-138">Via de portal om te kiezen bestaande resources vertelt u Azure voor het implementeren van de virtuele machine binnen de bestaande netwerk.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-138">By using the portal to choose existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="3e0a1-139">Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="3e0a1-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3e0a1-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e0a1-140">Next steps</span></span>

* [<span data-ttu-id="3e0a1-141">Een Azure Resource Manager-sjabloon gebruiken om een specifieke implementatie te maken</span><span class="sxs-lookup"><span data-stu-id="3e0a1-141">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="3e0a1-142">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="3e0a1-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="3e0a1-143">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="3e0a1-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
