---
title: Maak een Linux-VM in Azure met meerdere NIC's | Microsoft Docs
description: Informatie over het maken van een Linux-VM met meerdere NIC's gekoppeld met behulp van de Azure CLI 2.0 of Resource Manager-sjablonen.
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
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="3a5a0-103">Het maken van een virtuele Linux-machine in Azure met meerdere netwerk netwerkinterfacekaarten</span><span class="sxs-lookup"><span data-stu-id="3a5a0-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="3a5a0-104">U kunt een virtuele machine (VM) maken in Azure met meerdere virtuele netwerkinterfaces (NIC's) is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="3a5a0-105">Een veelvoorkomend scenario is om verschillende subnetten voor front-end en back-end-verbinding of een netwerk dat is toegewezen aan een oplossing met bewaking of back-up.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="3a5a0-106">Dit artikel wordt uitgelegd hoe een virtuele machine maken met meerdere NIC's gekoppeld en hoe toevoegen of verwijderen van NIC's van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="3a5a0-107">Voor gedetailleerde informatie, waaronder het maken van meerdere NIC's in uw eigen Bash-scripts Lees meer over [implementeren meerdere NIC's VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="3a5a0-108">Andere [VM-grootten](sizes.md) ondersteunen een verschillend aantal NIC's, dus het formaat van uw virtuele machine dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="3a5a0-109">Dit artikel wordt uitgelegd hoe u een virtuele machine maken met meerdere NIC's met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="3a5a0-110">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="3a5a0-111">Ondersteunende resources maken</span><span class="sxs-lookup"><span data-stu-id="3a5a0-111">Create supporting resources</span></span>
<span data-ttu-id="3a5a0-112">Installeer de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u aan op een Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3a5a0-113">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3a5a0-114">Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="3a5a0-115">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3a5a0-116">Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="3a5a0-117">Maken van het virtuele netwerk met [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="3a5a0-118">Het volgende voorbeeld wordt een virtueel netwerk met de naam *myVnet* en subnet met de naam *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="3a5a0-119">Een subnet maken voor de back-end-verkeer met [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="3a5a0-120">Het volgende voorbeeld wordt een subnet met de naam *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="3a5a0-121">Maken van een netwerkbeveiligingsgroep met [az netwerk nsg maken](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="3a5a0-122">Het volgende voorbeeld wordt een netwerkbeveiligingsgroep met de naam *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="3a5a0-123">Maak en configureer meerdere NIC 's</span><span class="sxs-lookup"><span data-stu-id="3a5a0-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="3a5a0-124">Maak twee NIC's met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3a5a0-125">Het volgende voorbeeld maakt u twee NIC's met de naam *myNic1* en *myNic2*, de netwerkbeveiligingsgroep verbonden met één NIC die verbinding maken met elk subnet:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="3a5a0-126">Een virtuele machine maken en koppelen van de NIC 's</span><span class="sxs-lookup"><span data-stu-id="3a5a0-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="3a5a0-127">Wanneer u de virtuele machine, maakt de NIC's geven u hebt gemaakt met `--nics`.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="3a5a0-128">U moet ook Wees voorzichtig wanneer u de VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="3a5a0-129">Er gelden beperkingen voor het totale aantal NIC's die u aan een virtuele machine toevoegen kunt.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="3a5a0-130">Lees meer over [Linux VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="3a5a0-131">Maak een VM met [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="3a5a0-132">Het volgende voorbeeld wordt een virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-132">The following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="3a5a0-133">Een NIC toevoegen aan een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="3a5a0-133">Add a NIC to a VM</span></span>
<span data-ttu-id="3a5a0-134">De vorige stappen kunt u een virtuele machine met meerdere NIC's gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="3a5a0-135">U kunt ook NIC's toevoegen aan een bestaande virtuele machine met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="3a5a0-136">Maken van een ander NIC met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3a5a0-137">Het volgende voorbeeld wordt een NIC met de naam *myNic3* verbonden met de back-end subnet netwerk beveiligingsgroep en in de vorige stappen hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="3a5a0-138">Als een NIC toevoegen aan een bestaande virtuele machine, met de virtuele machine eerst ongedaan [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="3a5a0-139">Het volgende voorbeeld de virtuele machine met de naam deallocates *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="3a5a0-140">Toevoegen van de NIC met [az vm nic toevoegen](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="3a5a0-141">Het volgende voorbeeld wordt *myNic3* naar *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="3a5a0-142">Start de virtuele machine met [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="3a5a0-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="3a5a0-143">Een NIC van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="3a5a0-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="3a5a0-144">Als u wilt verwijderen een NIC van een bestaande virtuele machine, met de virtuele machine eerst ongedaan [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="3a5a0-145">Het volgende voorbeeld de virtuele machine met de naam deallocates *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="3a5a0-146">Verwijderen van de NIC met [az vm nic verwijderen](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="3a5a0-147">Het volgende voorbeeld verwijdert u *myNic3* van *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="3a5a0-148">Start de virtuele machine met [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="3a5a0-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="3a5a0-149">Meerdere NIC's met behulp van Resource Manager-sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="3a5a0-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="3a5a0-150">Azure Resource Manager-sjablonen gebruiken declaratieve JSON-bestanden voor het definiëren van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="3a5a0-151">U vindt een [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="3a5a0-152">Resource Manager-sjablonen kunnen u meerdere exemplaren van een bron tijdens implementatie, zoals het maken van meerdere NIC's maken.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="3a5a0-153">U gebruikt *kopie* om op te geven van het aantal exemplaren te maken:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="3a5a0-154">Lees meer over [maken van meerdere exemplaren die gebruikmaken van *kopie*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="3a5a0-155">U kunt ook een `copyIndex()` toe te voegen vervolgens een nummer aan de naam van een resource, zodat u kunt maken `myNic1`, `myNic2`, enzovoort. Hier volgt een voorbeeld van de waarde voor de index:</span><span class="sxs-lookup"><span data-stu-id="3a5a0-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="3a5a0-156">U kunt een compleet voorbeeld van lezen [meerdere NIC's met behulp van Resource Manager-sjablonen maken](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="3a5a0-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a5a0-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a5a0-157">Next steps</span></span>
<span data-ttu-id="3a5a0-158">Bekijk [Linux VM-grootten](sizes.md) bij het maken van een virtuele machine met meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="3a5a0-159">Let op het maximum aantal NIC's die ondersteuning biedt voor elke VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="3a5a0-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 