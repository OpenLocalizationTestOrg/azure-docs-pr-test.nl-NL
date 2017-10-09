---
title: een kopie van uw Linux-VM met hello Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van uw Azure Linux virtuele machine met Azure CLI 1.0 Hallo Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="227a2-103">Maak een kopie van een virtuele Linux-machine uitgevoerd op Azure Hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="227a2-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="227a2-104">Dit artikel laat zien hoe een exemplaar van uw virtuele Azure-machine (VM) actieve Linux met toocreate Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="227a2-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="227a2-105">Eerst u Hallo-besturingssysteem en gegevens schijven tooa nieuwe container, worden overschreven klikt en vervolgens Hallo netwerkbronnen instellen en Hallo nieuwe virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="227a2-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="227a2-106">U kunt ook [uploaden en een virtuele machine maken van aangepaste schijfimage](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="227a2-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="227a2-107">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="227a2-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="227a2-108">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="227a2-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="227a2-109">Azure CLI 1.0 – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="227a2-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="227a2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="227a2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="227a2-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="227a2-111">Before you begin</span></span>
<span data-ttu-id="227a2-112">Zorg ervoor dat u voldoet aan de volgende vereisten voordat u de stappen Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="227a2-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="227a2-113">U hebt Hallo [Azure CLI](../../cli-install-nodejs.md) gedownload en geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="227a2-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="227a2-114">Ook moet u enkele gegevens over uw bestaande Azure Linux VM:</span><span class="sxs-lookup"><span data-stu-id="227a2-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="227a2-115">Informatie over het bron-VM</span><span class="sxs-lookup"><span data-stu-id="227a2-115">Source VM information</span></span> | <span data-ttu-id="227a2-116">Waar tooget deze</span><span class="sxs-lookup"><span data-stu-id="227a2-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="227a2-117">VM-naam</span><span class="sxs-lookup"><span data-stu-id="227a2-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="227a2-118">De naam van resourcegroep</span><span class="sxs-lookup"><span data-stu-id="227a2-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="227a2-119">Locatie</span><span class="sxs-lookup"><span data-stu-id="227a2-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="227a2-120">Naam van het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="227a2-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="227a2-121">Containernaam</span><span class="sxs-lookup"><span data-stu-id="227a2-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="227a2-122">Bronnaam VM VHD-bestand</span><span class="sxs-lookup"><span data-stu-id="227a2-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="227a2-123">U moet toomake enkele mogelijkheden over de nieuwe virtuele machine:   </span><span class="sxs-lookup"><span data-stu-id="227a2-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="227a2-124">-Containernaam   </span><span class="sxs-lookup"><span data-stu-id="227a2-124">-Container name    </span></span><br> <span data-ttu-id="227a2-125">VM - naam   </span><span class="sxs-lookup"><span data-stu-id="227a2-125">-VM name    </span></span><br> <span data-ttu-id="227a2-126">VM - grootte   </span><span class="sxs-lookup"><span data-stu-id="227a2-126">-VM size    </span></span><br> <span data-ttu-id="227a2-127">-vNet-naam   </span><span class="sxs-lookup"><span data-stu-id="227a2-127">-vNet name    </span></span><br> <span data-ttu-id="227a2-128">-Subnetnaam   </span><span class="sxs-lookup"><span data-stu-id="227a2-128">-SubNet name    </span></span><br> <span data-ttu-id="227a2-129">-IP-naam   </span><span class="sxs-lookup"><span data-stu-id="227a2-129">-IP Name    </span></span><br> <span data-ttu-id="227a2-130">De naam van de - NIC</span><span class="sxs-lookup"><span data-stu-id="227a2-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="227a2-131">Aanmelding en stel uw abonnement</span><span class="sxs-lookup"><span data-stu-id="227a2-131">Login and set your subscription</span></span>
1. <span data-ttu-id="227a2-132">Aanmelding toohello CLI.</span><span class="sxs-lookup"><span data-stu-id="227a2-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="227a2-133">Zorg ervoor dat u in de modus Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="227a2-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="227a2-134">Het juiste abonnement Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="227a2-134">Set hello correct subscription.</span></span> <span data-ttu-id="227a2-135">U kunt een lijst met azure-account toosee al uw abonnementen.</span><span class="sxs-lookup"><span data-stu-id="227a2-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="227a2-136">Hallo VM stoppen</span><span class="sxs-lookup"><span data-stu-id="227a2-136">Stop hello VM</span></span>
<span data-ttu-id="227a2-137">Stop en Hallo bron-VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="227a2-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="227a2-138">Lijst met azure vm tooget een lijst met alle Hallo VM's kunt u in uw abonnement en de namen van resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="227a2-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="227a2-139">Hallo VHD kopiëren</span><span class="sxs-lookup"><span data-stu-id="227a2-139">Copy hello VHD</span></span>
<span data-ttu-id="227a2-140">U kunt VHD Hallo kopiëren van Hallo bron toohello opslaglocatie Hallo met `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="227a2-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="227a2-141">In dit voorbeeld gaan we toocopy Hallo VHD toohello hetzelfde opslagaccount, maar een andere container.</span><span class="sxs-lookup"><span data-stu-id="227a2-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="227a2-142">toocopy hello VHD tooanother container in Hallo hetzelfde opslagaccount, type:</span><span class="sxs-lookup"><span data-stu-id="227a2-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="227a2-143">Hallo virtueel netwerk instellen voor uw nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="227a2-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="227a2-144">Stel een virtueel netwerk en de NIC in voor uw nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="227a2-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="227a2-145">Maken van nieuwe virtuele machine Hallo</span><span class="sxs-lookup"><span data-stu-id="227a2-145">Create hello new VM</span></span>
<span data-ttu-id="227a2-146">U kunt nu een virtuele machine maken van de geüploade virtuele schijf [met behulp van een resource manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) of via Hallo CLI door te geven Hallo URI tooyour schijf gekopieerd door te typen:</span><span class="sxs-lookup"><span data-stu-id="227a2-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="227a2-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="227a2-147">Next steps</span></span>
<span data-ttu-id="227a2-148">toolearn hoe toouse Azure CLI toomanage uw nieuwe virtuele machine, Zie [Azure CLI-opdrachten voor hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="227a2-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

