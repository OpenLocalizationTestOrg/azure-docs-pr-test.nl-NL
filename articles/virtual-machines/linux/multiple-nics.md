---
title: een Linux-VM in Azure met meerdere NIC's aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Linux-VM met meerdere NIC's gekoppeld tooit hello Azure CLI 2.0 of Resource Manager-sjablonen.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="4295b-103">Hoe toocreate virtuele Linux-machine in Azure met meerdere netwerk netwerkinterfacekaarten</span><span class="sxs-lookup"><span data-stu-id="4295b-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="4295b-104">U kunt een virtuele machine (VM) maken in Azure die meerdere virtuele netwerkinterfaces (NIC's) die zijn gekoppeld tooit heeft.</span><span class="sxs-lookup"><span data-stu-id="4295b-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="4295b-105">Een veelvoorkomend scenario toohave verschillende subnetten voor front-end en back-end-connectiviteit is of een netwerk toegewezen tooa bewaking of back-upoplossing.</span><span class="sxs-lookup"><span data-stu-id="4295b-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="4295b-106">Dit artikel wordt uitgelegd hoe toocreate met meerdere NIC's een virtuele machine gekoppeld tooit en hoe tooadd of verwijder NIC's van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4295b-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="4295b-107">Voor gedetailleerde informatie, met inbegrip van hoe toocreate meerdere NIC's in uw eigen Bash-scripts, lees meer over [implementeren meerdere NIC's VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4295b-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="4295b-108">Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="4295b-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="4295b-109">Dit artikel wordt uitgelegd hoe toocreate een virtuele machine met meerdere NIC's met Azure CLI 2.0 Hallo.</span><span class="sxs-lookup"><span data-stu-id="4295b-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="4295b-110">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4295b-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="4295b-111">Ondersteunende resources maken</span><span class="sxs-lookup"><span data-stu-id="4295b-111">Create supporting resources</span></span>
<span data-ttu-id="4295b-112">Meest recente installatie Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4295b-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4295b-113">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="4295b-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4295b-114">Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="4295b-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="4295b-115">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4295b-116">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="4295b-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4295b-117">Virtueel netwerk met Hallo maken [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="4295b-118">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en subnet met de naam *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="4295b-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="4295b-119">Maak een subnet voor back-end-verkeer Hallo met [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="4295b-120">Hallo volgende voorbeeld wordt een subnet met de naam *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="4295b-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="4295b-121">Maken van een netwerkbeveiligingsgroep met [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="4295b-122">Hallo volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="4295b-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="4295b-123">Maak en configureer meerdere NIC 's</span><span class="sxs-lookup"><span data-stu-id="4295b-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="4295b-124">Maak twee NIC's met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="4295b-125">Hallo volgende voorbeeld maakt u twee NIC's met de naam *myNic1* en *myNic2*, met elkaar verbonden Hallo netwerkbeveiligingsgroep, met één NIC tooeach subnet verbinding te maken:</span><span class="sxs-lookup"><span data-stu-id="4295b-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="4295b-126">Een virtuele machine maken en koppelen van Hallo NIC 's</span><span class="sxs-lookup"><span data-stu-id="4295b-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="4295b-127">Wanneer u Hallo VM maakt, geef Hallo NIC's u hebt gemaakt met `--nics`.</span><span class="sxs-lookup"><span data-stu-id="4295b-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="4295b-128">U moet ook tootake voorzichtig wanneer u Hallo VM-grootte selecteert.</span><span class="sxs-lookup"><span data-stu-id="4295b-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="4295b-129">Er gelden beperkingen voor Hallo kunt u het totale aantal NIC's die u tooa VM kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4295b-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="4295b-130">Lees meer over [Linux VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4295b-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="4295b-131">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="4295b-132">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4295b-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="4295b-133">Toevoegen van een NIC tooa VM</span><span class="sxs-lookup"><span data-stu-id="4295b-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="4295b-134">de vorige stappen Hallo gemaakt van een virtuele machine met meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="4295b-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="4295b-135">U kunt ook NIC's tooan bestaande VM Hello Azure CLI 2.0 toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4295b-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="4295b-136">Maken van een ander NIC met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="4295b-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="4295b-137">Hallo volgende voorbeeld wordt een NIC met de naam *myNic3* toohello back-end-subnet en netwerkbeveiligingsgroep gemaakt in de vorige stappen Hallo verbonden:</span><span class="sxs-lookup"><span data-stu-id="4295b-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="4295b-138">een NIC tooan tooadd bestaande VM eerst ongedaan Hallo VM met [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="4295b-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="4295b-139">Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4295b-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4295b-140">Voeg Hallo NIC met [az vm nic toevoegen](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="4295b-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="4295b-141">Hallo volgende voorbeeld wordt *myNic3* te*myVM*:</span><span class="sxs-lookup"><span data-stu-id="4295b-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="4295b-142">Start met virtuele machine Hallo [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="4295b-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="4295b-143">Een NIC van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="4295b-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="4295b-144">een NIC van een bestaande VM tooremove eerst Hallo VM ongedaan gemaakt met [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="4295b-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="4295b-145">Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4295b-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4295b-146">Verwijder Hallo NIC met [az vm nic verwijderen](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="4295b-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="4295b-147">Hallo volgende voorbeeld wordt verwijderd *myNic3* van *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4295b-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="4295b-148">Start met virtuele machine Hallo [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="4295b-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="4295b-149">Meerdere NIC's met behulp van Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="4295b-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="4295b-150">Azure Resource Manager-sjablonen gebruiken declaratieve JSON-bestanden toodefine uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="4295b-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="4295b-151">U vindt een [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4295b-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="4295b-152">Resource Manager-sjablonen bieden een manier toocreate meerdere exemplaren van een bron tijdens implementatie, zoals meerdere NIC's maken.</span><span class="sxs-lookup"><span data-stu-id="4295b-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="4295b-153">U gebruikt *kopie* toospecify Hallo aantal exemplaren toocreate:</span><span class="sxs-lookup"><span data-stu-id="4295b-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="4295b-154">Lees meer over [maken van meerdere exemplaren die gebruikmaken van *kopie*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="4295b-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="4295b-155">U kunt ook een `copyIndex()` toothen toevoeg-een nummer tooa resourcenaam, zodat u toocreate `myNic1`, `myNic2`, enzovoort Hallo hieronder vindt u een voorbeeld van de indexwaarde Hallo:</span><span class="sxs-lookup"><span data-stu-id="4295b-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="4295b-156">U kunt een compleet voorbeeld van lezen [meerdere NIC's met behulp van Resource Manager-sjablonen maken](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="4295b-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4295b-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4295b-157">Next steps</span></span>
<span data-ttu-id="4295b-158">Bekijk [Linux VM-grootten](sizes.md) bij het toocreating met meerdere NIC's een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4295b-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="4295b-159">Betalen aandacht toohello maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="4295b-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
