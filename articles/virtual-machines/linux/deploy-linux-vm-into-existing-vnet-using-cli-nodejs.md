---
title: Implementeren van virtuele Linux-machines in de bestaande netwerk met Azure CLI 1.0 | Microsoft Docs
description: Het implementeren van een Linux-VM naar een bestaand virtueel netwerk met behulp van de Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="a4441-103">Het implementeren van een virtuele Linux-machine in Azure een bestaand virtueel netwerk met de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a4441-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="a4441-104">In dit artikel laat zien hoe Azure CLI 1.0 gebruiken voor het implementeren van een virtuele machine (VM) in een bestaand virtueel netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="a4441-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="a4441-105">De vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="a4441-105">The requirements are:</span></span>

- [<span data-ttu-id="a4441-106">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a4441-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="a4441-107">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="a4441-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a4441-108">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="a4441-108">CLI versions to complete the task</span></span>
<span data-ttu-id="a4441-109">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="a4441-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a4441-110">[Azure CLI 1.0](#quick-commands) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="a4441-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a4441-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="a4441-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="a4441-112">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="a4441-112">Quick Commands</span></span>

<span data-ttu-id="a4441-113">Als u de taak snel uitvoeren moet, wordt de volgende sectie de opdrachten die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="a4441-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="a4441-114">Meer gedetailleerde informatie en context voor elke stap u de rest van het document vindt [vanaf hier](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a4441-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="a4441-115">Randvoorwaarden voor: Resourcegroep, VNet, NSG met SSH inkomende Subnet.</span><span class="sxs-lookup"><span data-stu-id="a4441-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="a4441-116">Geen voorbeelden vervangen door uw eigen instellingen.</span><span class="sxs-lookup"><span data-stu-id="a4441-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="a4441-117">Implementeer de virtuele machine in de infrastructuur van het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="a4441-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="a4441-118">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="a4441-118">Detailed walkthrough</span></span>

<span data-ttu-id="a4441-119">Azure activa, zoals de VNets en netwerkbeveiligingsgroepen moeten statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="a4441-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="a4441-120">Zodra een VNet is geïmplementeerd, kan dit opnieuw gebruikt door nieuwe implementaties zonder een ongewenst is van invloed op de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="a4441-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="a4441-121">Denk na over een VNet dat een netwerkswitch traditionele hardware.</span><span class="sxs-lookup"><span data-stu-id="a4441-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="a4441-122">U moet niet een geheel nieuwe hardwareswitch configureren met elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="a4441-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="a4441-123">U kunt blijven implementeren nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen die zijn vereist tijdens de levensduur van het VNet met een juist geconfigureerde VNet.</span><span class="sxs-lookup"><span data-stu-id="a4441-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="a4441-124">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="a4441-124">Create the resource group</span></span>

<span data-ttu-id="a4441-125">Maak eerst een resourcegroep te organiseren alles wat die u in dit scenario maakt.</span><span class="sxs-lookup"><span data-stu-id="a4441-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="a4441-126">Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a4441-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="a4441-127">Het VNet maken</span><span class="sxs-lookup"><span data-stu-id="a4441-127">Create the VNet</span></span>

<span data-ttu-id="a4441-128">De eerste stap is het bouwen van een VNet Start de virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="a4441-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="a4441-129">Het VNet bevat één subnet voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="a4441-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="a4441-130">Zie voor meer informatie over Azure VNets [een virtueel netwerk maken met behulp van de Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a4441-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="a4441-131">De netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="a4441-131">Create the network security group</span></span>

<span data-ttu-id="a4441-132">Het subnet is gebouwd achter een bestaand netwerk beveiligingsgroep maken zodat de netwerkbeveiligingsgroep voor het subnet.</span><span class="sxs-lookup"><span data-stu-id="a4441-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="a4441-133">Beveiligingsgroepen voor Azure-netwerk zijn equivalent aan een firewall op de netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="a4441-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="a4441-134">Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [netwerk beveiligingsgroepen maken in de Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a4441-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="a4441-135">Regel voor geven van een binnenkomende SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="a4441-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="a4441-136">De virtuele machine moet toegang via het internet, zodat een regel binnenkomende poort 22-verkeer op de virtuele machine via het netwerk worden doorgegeven aan poort 22 nodig is.</span><span class="sxs-lookup"><span data-stu-id="a4441-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="a4441-137">Voeg een subnet toe aan het VNet</span><span class="sxs-lookup"><span data-stu-id="a4441-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="a4441-138">Virtuele machines binnen het VNet moeten zich bevinden in een subnet.</span><span class="sxs-lookup"><span data-stu-id="a4441-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="a4441-139">Elke VNet kan meerdere subnetten hebben.</span><span class="sxs-lookup"><span data-stu-id="a4441-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="a4441-140">Het subnet te maken en koppelen aan de netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="a4441-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="a4441-141">Het Subnet is nu toegevoegd in het VNet en die zijn gekoppeld aan de netwerkbeveiligingsgroep en de regelset.</span><span class="sxs-lookup"><span data-stu-id="a4441-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="a4441-142">Een VNic toevoegen aan het subnet</span><span class="sxs-lookup"><span data-stu-id="a4441-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="a4441-143">Virtueel-netwerkkaarten (VNics) zijn belangrijk omdat u ze hergebruiken kunt door deze te verbinden met andere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a4441-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="a4441-144">Deze aanpak houdt de VNic als statische resource terwijl de virtuele machines kunnen tijdelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="a4441-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="a4441-145">Een VNic maken en deze koppelen aan het subnet in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4441-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="a4441-146">Implementeer de virtuele machine in het VNet en het NSG</span><span class="sxs-lookup"><span data-stu-id="a4441-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="a4441-147">U hebt nu een VNet en het subnet in dit VNet en een netwerkbeveiligingsgroep ter bescherming van het subnet blokkeert al het binnenkomende verkeer behalve poort 22 voor SSH fungeert.</span><span class="sxs-lookup"><span data-stu-id="a4441-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="a4441-148">De virtuele machine kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="a4441-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="a4441-149">Met de Azure CLI, en de `azure vm create` opdracht, de Linux-VM wordt geïmplementeerd op de bestaande Azure-resourcegroep, VNet, Subnet en VNic.</span><span class="sxs-lookup"><span data-stu-id="a4441-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="a4441-150">Zie voor meer informatie over een volledige virtuele machine implementeren met behulp van de CLI [een volledige Linux-omgeving maken met behulp van de Azure CLI](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="a4441-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="a4441-151">Met behulp van de vlaggen CLI aan te roepen bestaande bronnen, vertelt u Azure voor het implementeren van de virtuele machine binnen de bestaande netwerk.</span><span class="sxs-lookup"><span data-stu-id="a4441-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="a4441-152">Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="a4441-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a4441-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4441-153">Next steps</span></span>

* [<span data-ttu-id="a4441-154">Een Azure Resource Manager-sjabloon gebruiken om een specifieke implementatie te maken</span><span class="sxs-lookup"><span data-stu-id="a4441-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="a4441-155">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="a4441-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="a4441-156">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="a4441-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
