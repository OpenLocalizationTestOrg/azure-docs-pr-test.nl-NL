---
title: aaaDeploy virtuele Linux-machines in bestaande netwerk met Azure CLI 1.0 | Microsoft Docs
description: Hoe een Linux-VM naar een bestaand virtueel netwerk met behulp van toodeploy hello Azure CLI 1.0
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
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="ba04c-103">Hoe een virtuele Linux-machine in Azure een bestaand virtueel netwerk met Azure CLI 1.0 Hallo toodeploy</span><span class="sxs-lookup"><span data-stu-id="ba04c-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="ba04c-104">Dit artikel ziet u hoe toouse Azure CLI 1.0 toodeploy een virtuele machine (VM) in een bestaand virtueel netwerk (VNet).</span><span class="sxs-lookup"><span data-stu-id="ba04c-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="ba04c-105">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="ba04c-105">hello requirements are:</span></span>

- [<span data-ttu-id="ba04c-106">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ba04c-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="ba04c-107">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="ba04c-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ba04c-108">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="ba04c-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="ba04c-109">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ba04c-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="ba04c-110">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="ba04c-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ba04c-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="ba04c-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ba04c-112">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="ba04c-112">Quick Commands</span></span>

<span data-ttu-id="ba04c-113">Als u moet tooquickly Hallo taak, Hallo sectie volgen details Hallo opdrachten die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="ba04c-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="ba04c-114">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="ba04c-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="ba04c-115">Randvoorwaarden voor: Resourcegroep, VNet, NSG met SSH inkomende Subnet.</span><span class="sxs-lookup"><span data-stu-id="ba04c-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="ba04c-116">Geen voorbeelden vervangen door uw eigen instellingen.</span><span class="sxs-lookup"><span data-stu-id="ba04c-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="ba04c-117">Hallo VM in Hallo virtuele netwerkinfrastructuur implementeren</span><span class="sxs-lookup"><span data-stu-id="ba04c-117">Deploy hello VM into hello virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="ba04c-118">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="ba04c-118">Detailed walkthrough</span></span>

<span data-ttu-id="ba04c-119">Azure activa zoals Hallo VNets en netwerkbeveiligingsgroepen moeten statisch zijn en resources die zelden zijn geïmplementeerd langer bewaard moeten blijven.</span><span class="sxs-lookup"><span data-stu-id="ba04c-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="ba04c-120">Zodra een VNet is geïmplementeerd, kan opnieuw door nieuwe implementaties zonder een nadelige invloed toohello infrastructuur worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ba04c-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="ba04c-121">Denk na over een VNet dat een netwerkswitch traditionele hardware.</span><span class="sxs-lookup"><span data-stu-id="ba04c-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="ba04c-122">U hoeft dan niet een geheel nieuwe hardware overschakelen met elke implementatie tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ba04c-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="ba04c-123">Met een juist geconfigureerde VNet, kunt u blijven toodeploy nieuwe servers in dit VNet steeds met enkele eventuele wijzigingen gedurende de levensduur Hallo Hallo VNet vereist.</span><span class="sxs-lookup"><span data-stu-id="ba04c-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="ba04c-124">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="ba04c-124">Create hello resource group</span></span>

<span data-ttu-id="ba04c-125">Maak eerst een groep resource tooorganize alles wat die u in dit scenario maakt.</span><span class="sxs-lookup"><span data-stu-id="ba04c-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="ba04c-126">Zie voor meer informatie over resourcegroepen [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ba04c-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="ba04c-127">Hallo VNet maken</span><span class="sxs-lookup"><span data-stu-id="ba04c-127">Create hello VNet</span></span>

<span data-ttu-id="ba04c-128">de eerste stap Hallo is toobuild een VNet-toolaunch Hallo VM's in.</span><span class="sxs-lookup"><span data-stu-id="ba04c-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="ba04c-129">Hallo VNet bevat één subnet voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="ba04c-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="ba04c-130">Zie voor meer informatie over Azure VNets [een virtueel netwerk maken met behulp van hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ba04c-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="ba04c-131">Hallo netwerkbeveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="ba04c-131">Create hello network security group</span></span>

<span data-ttu-id="ba04c-132">Hallo-subnet is gebouwd achter een bestaande netwerkbeveiligingsgroep dus bouwen Hallo netwerkbeveiligingsgroep voordat Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="ba04c-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="ba04c-133">Beveiligingsgroepen voor Azure-netwerk zijn equivalent tooa firewall op Hallo netwerklaag.</span><span class="sxs-lookup"><span data-stu-id="ba04c-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="ba04c-134">Zie voor meer informatie over Azure netwerkbeveiligingsgroepen [hoe toocreate netwerk beveiligingsgroepen in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ba04c-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="ba04c-135">Regel voor geven van een binnenkomende SSH toevoegen</span><span class="sxs-lookup"><span data-stu-id="ba04c-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="ba04c-136">Hallo VM moet toegang vanaf Hallo internet zodat een regel voor het toestaan van binnenkomende poort 22 verkeer toobe Hallo netwerk tooport 22 op Hallo VM doorgegeven nodig is.</span><span class="sxs-lookup"><span data-stu-id="ba04c-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="ba04c-137">Voeg een subnet toohello VNet</span><span class="sxs-lookup"><span data-stu-id="ba04c-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="ba04c-138">Virtuele machines binnen Hallo VNet moeten zich bevinden in een subnet.</span><span class="sxs-lookup"><span data-stu-id="ba04c-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="ba04c-139">Elke VNet kan meerdere subnetten hebben.</span><span class="sxs-lookup"><span data-stu-id="ba04c-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="ba04c-140">Hallo subnet maken en koppelen aan de netwerkbeveiligingsgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba04c-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="ba04c-141">Hallo Subnet is nu toegevoegd in Hallo VNet en die zijn gekoppeld aan netwerkbeveiligingsgroep hello en regel.</span><span class="sxs-lookup"><span data-stu-id="ba04c-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="ba04c-142">Een VNic toohello subnet toevoegen</span><span class="sxs-lookup"><span data-stu-id="ba04c-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="ba04c-143">Virtueel-netwerkkaarten (VNics) zijn belangrijk omdat u ze hergebruiken kunt door deze toodifferent virtuele machines te verbinden.</span><span class="sxs-lookup"><span data-stu-id="ba04c-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="ba04c-144">Deze aanpak houdt Hallo VNic als statische resource Hallo VMs tijdelijke kan zijn.</span><span class="sxs-lookup"><span data-stu-id="ba04c-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="ba04c-145">Een VNic maken en deze koppelen aan Hallo subnet in de vorige stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ba04c-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="ba04c-146">Hallo VM in Hallo VNet en NSG implementeren</span><span class="sxs-lookup"><span data-stu-id="ba04c-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="ba04c-147">U hebt nu een VNet en het subnet in dit VNet en een netwerkbeveiligingsgroep tooprotect Hallo subnet blokkeert al het binnenkomende verkeer behalve poort 22 voor SSH fungeert.</span><span class="sxs-lookup"><span data-stu-id="ba04c-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="ba04c-148">Hallo VM kan nu worden geïmplementeerd in deze bestaande netwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="ba04c-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="ba04c-149">Met behulp van Azure CLI Hallo en Hallo `azure vm create` opdracht Hallo Linux VM geïmplementeerde toohello bestaande Azure-resourcegroep, VNet Subnet en VNic is.</span><span class="sxs-lookup"><span data-stu-id="ba04c-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="ba04c-150">Zie voor meer informatie over het gebruik van Hallo CLI toodeploy een volledige virtuele machine [een volledige Linux-omgeving maken met behulp van hello Azure CLI](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="ba04c-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="ba04c-151">Met behulp van Hallo vlaggen CLI toocall uit bestaande resources instrueren van Azure toodeploy Hallo VM binnen de bestaande netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba04c-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="ba04c-152">Zodra een VNet en een subnet is geïmplementeerd, kunnen ze als statisch of permanente resources binnen uw Azure-regio worden gelaten.</span><span class="sxs-lookup"><span data-stu-id="ba04c-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ba04c-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ba04c-153">Next steps</span></span>

* [<span data-ttu-id="ba04c-154">Een Azure Resource Manager-sjabloon toocreate een specifieke implementatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="ba04c-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="ba04c-155">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="ba04c-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="ba04c-156">Linux-VM in Azure met behulp van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="ba04c-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
