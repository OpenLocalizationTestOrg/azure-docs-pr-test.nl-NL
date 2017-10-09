---
title: een Linux-VM met behulp van Azure CLI 2.0 aaaCopy | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van uw Azure Linux virtuele machine met behulp van Azure CLI 2.0 en schijven beheerd.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="75992-103">Maak een kopie van een Linux-VM met behulp van Azure CLI 2.0 en schijven beheerd</span><span class="sxs-lookup"><span data-stu-id="75992-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="75992-104">Dit artikel laat zien hoe een kopie van uw Azure virtuele machine (VM) met behulp van Linux toocreate hello Azure CLI 2.0 en hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="75992-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="75992-105">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75992-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="75992-106">U kunt ook [uploaden en een virtuele machine maken vanaf een VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75992-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75992-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="75992-107">Prerequisites</span></span>


-   <span data-ttu-id="75992-108">Installeer [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="75992-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="75992-109">Meld u aan tooan Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="75992-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="75992-110">Een virtuele machine van Azure toouse als Hallo bron voor uw exemplaar hebben.</span><span class="sxs-lookup"><span data-stu-id="75992-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="75992-111">Stap 1: Hallo bron-VM stoppen</span><span class="sxs-lookup"><span data-stu-id="75992-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="75992-112">Hallo bron-VM met behulp van toewijzing [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="75992-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="75992-113">Hallo volgende voorbeeld deallocates Hallo VM met de naam **myVM** in de resourcegroep Hallo **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="75992-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="75992-114">Stap 2: Kopieer Hallo bron-VM</span><span class="sxs-lookup"><span data-stu-id="75992-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="75992-115">toocopy een virtuele machine, maakt u een kopie van Hallo onderliggende virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="75992-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="75992-116">Dit proces maakt een gespecialiseerde VHD als een schijf beheerd Hallo met dezelfde configuratie en instellingen als Hallo bron-VM.</span><span class="sxs-lookup"><span data-stu-id="75992-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="75992-117">Zie [Overzicht van Azure Managed Disks](../windows/managed-disks-overview.md) voor meer informatie over Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="75992-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="75992-118">Lijst van de OS-schijf met de naam van elke virtuele machine en Hallo [az vm lijst](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="75992-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="75992-119">Hallo volgende voorbeeld worden alle virtuele machines in de resourcegroep met de naam **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="75992-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="75992-120">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="75992-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="75992-121">Hallo diskette kopiëren door het maken van een nieuwe schijf met beheerd [az schijf maken](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="75992-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="75992-122">Hallo volgende voorbeeld wordt een schijf met de naam **myCopiedDisk** beheerd schijf met de naam van Hallo **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="75992-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="75992-123">Hallo beheerd schijven nu in de resourcegroep controleren met behulp van [az Schijflijst](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="75992-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="75992-124">Hallo volgende voorbeeld worden beheerd Hallo schijven in de resourcegroep Hallo met de naam **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="75992-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="75992-125">Overslaan te[' stap 3: een virtueel netwerk instellen '](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="75992-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="75992-126">Stap 3: Een virtueel netwerk instellen</span><span class="sxs-lookup"><span data-stu-id="75992-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="75992-127">Hallo Maak volgende optionele stappen een nieuw virtueel netwerk, subnet, openbare IP-adres en virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="75992-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="75992-128">Als u een virtuele machine voor het oplossen van problemen of aanvullende implementaties kopieert, wilt u mogelijk niet toouse een virtuele machine in een bestaand virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="75992-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="75992-129">Als u een virtuele-netwerkinfrastructuur toocreate wilt voor de gekopieerde virtuele machines, Hallo Volg volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="75992-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="75992-130">Als u een virtueel netwerk toocreate niet wilt, gaat u verder te[stap 4: een virtuele machine maken](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="75992-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="75992-131">Hallo virtueel netwerk maken met behulp van [az network vnet maken](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="75992-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="75992-132">Hallo volgende voorbeeld wordt een virtueel netwerk met de naam **myVnet** en een subnet met de naam **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="75992-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="75992-133">Maken van een openbaar IP-adres met behulp van [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="75992-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="75992-134">Hallo volgende voorbeeld maakt u een openbaar IP-adres met de naam **myPublicIP** met Hallo DNS-naam van **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="75992-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="75992-135">(Hallo DNS-naam moet uniek zijn, dus een unieke naam opgeven.)</span><span class="sxs-lookup"><span data-stu-id="75992-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="75992-136">Maak Hallo NIC met [az netwerk nic maken](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="75992-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="75992-137">Hallo volgende voorbeeld wordt een NIC met de naam **myNic** die gekoppelde toothe **mySubnet** subnet:</span><span class="sxs-lookup"><span data-stu-id="75992-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="75992-138">Stap 4: Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="75992-138">Step 4: Create a VM</span></span>

<span data-ttu-id="75992-139">U kunt nu een virtuele machine maken met behulp van [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="75992-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="75992-140">Geef Hallo gekopieerd toouse als Hallo OS-schijf beheerde schijven (--koppelen-os-schijf), als volgt:</span><span class="sxs-lookup"><span data-stu-id="75992-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="75992-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="75992-141">Next steps</span></span>

<span data-ttu-id="75992-142">toolearn hoe toouse Azure CLI toomanage uw nieuwe VM Zie [Azure CLI-opdrachten voor hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="75992-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
