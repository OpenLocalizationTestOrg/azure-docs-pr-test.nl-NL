---
title: een Linux-VM in Azure met meerdere NIC's aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Linux-VM met meerdere NIC's gekoppeld tooit hello Azure CLI of Resource Manager-sjablonen.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="1769c-103">Een virtuele Linux-machine maken met meerdere NIC's met behulp van hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1769c-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1769c-104">U kunt een virtuele machine (VM) maken in Azure die meerdere virtuele netwerkinterfaces (NIC's) die zijn gekoppeld tooit heeft.</span><span class="sxs-lookup"><span data-stu-id="1769c-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="1769c-105">Een veelvoorkomend scenario toohave verschillende subnetten voor front-end en back-end-connectiviteit is of een netwerk toegewezen tooa bewaking of back-upoplossing.</span><span class="sxs-lookup"><span data-stu-id="1769c-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="1769c-106">Dit artikel vindt u een virtuele machine met meerdere NIC's gekoppeld tooit toocreate snelle opdrachten.</span><span class="sxs-lookup"><span data-stu-id="1769c-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="1769c-107">Voor gedetailleerde informatie, met inbegrip van hoe toocreate meerdere NIC's in uw eigen Bash-scripts, lees meer over [implementeren meerdere NIC's VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1769c-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="1769c-108">Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="1769c-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="1769c-109">Wanneer u een virtuele machine maken: u kunt geen NIC's tooan bestaande VM Hello Azure CLI 1.0 toevoegen, moet u meerdere NIC's koppelen.</span><span class="sxs-lookup"><span data-stu-id="1769c-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="1769c-110">U kunt [toegevoegd netwerkkaarten tooan bestaande VM Hello Azure CLI 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="1769c-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="1769c-111">U kunt ook [maken van een virtuele machine op basis van de oorspronkelijke virtuele schijven Hallo](copy-vm.md) en meerdere NIC's maken als u Hallo VM implementeren.</span><span class="sxs-lookup"><span data-stu-id="1769c-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1769c-112">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="1769c-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1769c-113">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1769c-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1769c-114">[Azure CLI 1.0](#create-supporting-resources) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="1769c-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1769c-115">[Azure CLI 2.0](multiple-nics.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="1769c-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="1769c-116">Ondersteunende resources maken</span><span class="sxs-lookup"><span data-stu-id="1769c-116">Create supporting resources</span></span>
<span data-ttu-id="1769c-117">Zorg ervoor dat u Hallo hebt [Azure CLI](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="1769c-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1769c-118">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="1769c-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1769c-119">Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1769c-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="1769c-120">Maak eerst een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1769c-120">First, create a resource group.</span></span> <span data-ttu-id="1769c-121">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="1769c-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="1769c-122">Maak een account opslag toohold uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1769c-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="1769c-123">Hallo volgende voorbeeld wordt een opslagaccount met de naam *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="1769c-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="1769c-124">Een virtueel netwerk tooconnect uw virtuele machines te maken.</span><span class="sxs-lookup"><span data-stu-id="1769c-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="1769c-125">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* met een adresvoorvoegsel van *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="1769c-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="1769c-126">Maken van twee virtuele netwerksubnetten: één voor verkeer van de front-end- en één voor verkeer van de back-end.</span><span class="sxs-lookup"><span data-stu-id="1769c-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="1769c-127">Hallo volgende voorbeeld maakt u twee subnetten, met de naam *mySubnetFrontEnd* en *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="1769c-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="1769c-128">Maak en configureer meerdere NIC 's</span><span class="sxs-lookup"><span data-stu-id="1769c-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="1769c-129">Vindt u meer informatie over [implementeren meerdere NIC's met behulp van Azure CLI Hallo](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), inclusief scripts Hallo proces toocreate doorlopen van alle Hallo NIC's.</span><span class="sxs-lookup"><span data-stu-id="1769c-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="1769c-130">Hallo volgende voorbeeld maakt u twee NIC's met de naam *myNic1* en *myNic2*, met één NIC tooeach subnet verbinding te maken:</span><span class="sxs-lookup"><span data-stu-id="1769c-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="1769c-131">Maakt u gewoonlijk ook een [Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) of [netwerktaakverdeler](../../load-balancer/load-balancer-overview.md) toohelp beheren en distribueren van verkeer tussen uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1769c-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="1769c-132">Hallo volgende voorbeeld wordt een Netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1769c-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="1769c-133">BIND uw NIC's toohello Netwerkbeveiligingsgroep met `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="1769c-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="1769c-134">Hallo volgende voorbeeld wordt gebonden *myNic1* en *myNic2* met *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1769c-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="1769c-135">Een virtuele machine maken en koppelen van Hallo NIC 's</span><span class="sxs-lookup"><span data-stu-id="1769c-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="1769c-136">Bij het maken van VM Hallo opgeven u nu meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="1769c-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="1769c-137">In plaats daarvan met `--nic-name` tooprovide één NIC, gebruik in plaats daarvan u `--nic-names` en een door komma's gescheiden lijst met NIC's bieden.</span><span class="sxs-lookup"><span data-stu-id="1769c-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="1769c-138">U moet ook tootake voorzichtig wanneer u Hallo VM-grootte selecteert.</span><span class="sxs-lookup"><span data-stu-id="1769c-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="1769c-139">Er gelden beperkingen voor Hallo kunt u het totale aantal NIC's die u tooa VM kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1769c-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="1769c-140">Lees meer over [Linux VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1769c-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="1769c-141">Hallo volgende voorbeeld laat zien hoe toospecify meerdere NIC's en klik vervolgens op een virtuele machine het formaat dat ondersteunt het gebruik van meerdere NIC's (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="1769c-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="1769c-142">Meerdere NIC's met behulp van Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="1769c-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="1769c-143">Azure Resource Manager-sjablonen gebruiken declaratieve JSON-bestanden toodefine uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="1769c-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="1769c-144">U vindt een [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1769c-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1769c-145">Resource Manager-sjablonen bieden een manier toocreate meerdere exemplaren van een bron tijdens implementatie, zoals meerdere NIC's maken.</span><span class="sxs-lookup"><span data-stu-id="1769c-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="1769c-146">U gebruikt *kopie* toospecify Hallo aantal exemplaren toocreate:</span><span class="sxs-lookup"><span data-stu-id="1769c-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="1769c-147">Lees meer over [maken van meerdere exemplaren die gebruikmaken van *kopie*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1769c-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="1769c-148">U kunt ook een `copyIndex()` toothen toevoeg-een nummer tooa resourcenaam, zodat u toocreate `myNic1`, `myNic2`, enzovoort Hallo hieronder vindt u een voorbeeld van de indexwaarde Hallo:</span><span class="sxs-lookup"><span data-stu-id="1769c-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="1769c-149">U kunt een compleet voorbeeld van lezen [meerdere NIC's met behulp van Resource Manager-sjablonen maken](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1769c-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1769c-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1769c-150">Next steps</span></span>
<span data-ttu-id="1769c-151">Zorg ervoor dat tooreview [Linux VM-grootten](sizes.md) bij het toocreating met meerdere NIC's een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1769c-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="1769c-152">Betalen aandacht toohello maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="1769c-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="1769c-153">Houd er rekening mee dat u aanvullende NIC's tooan bestaande VM niet toevoegen, moet u alle Hallo NIC's maken bij het implementeren van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="1769c-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="1769c-154">Wees voorzichtig bij het plannen van uw implementaties toomake ervoor dat u alle Hallo vereist netwerkverbinding vanaf Hallo begin hebt.</span><span class="sxs-lookup"><span data-stu-id="1769c-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

