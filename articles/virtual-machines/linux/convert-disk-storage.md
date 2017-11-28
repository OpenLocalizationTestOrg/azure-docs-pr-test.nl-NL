---
title: Converteren van Azure storage van de schijven van standaard beheerd naar premium, en vice versa | Microsoft Docs
description: Het converteren van Azure beheerd schijven opslag van standaard naar premium en omgekeerd, met behulp van Azure CLI.
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 0380b4aaa23b4aaba4c67d05e2d62f3ef41d6a32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="b02a2-103">Converteren van Azure storage van de schijven van standaard beheerd naar premium, en omgekeerd</span><span class="sxs-lookup"><span data-stu-id="b02a2-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="b02a2-104">Beheerde schijven biedt twee opties voor opslag: [Premium](../../storage/storage-premium-storage.md) (SSD-gebaseerde) en [standaard](../../storage/storage-standard-storage.md) (gebaseerd op harde schijf).</span><span class="sxs-lookup"><span data-stu-id="b02a2-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="b02a2-105">Hiermee kunt u eenvoudig schakelen tussen de twee opties met minimale downtime op basis van uw prestatievereisten past.</span><span class="sxs-lookup"><span data-stu-id="b02a2-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="b02a2-106">Deze mogelijkheid is niet beschikbaar voor niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="b02a2-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="b02a2-107">Maar u kunt eenvoudig [converteren naar beheerde schijven](convert-unmanaged-to-managed-disks.md) eenvoudig schakelen tussen de twee opties.</span><span class="sxs-lookup"><span data-stu-id="b02a2-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="b02a2-108">In dit artikel leest u hoe beheerde schijven van standard converteren naar premium, en vice versa met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b02a2-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="b02a2-109">Als u wilt installeren of upgraden, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b02a2-109">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b02a2-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b02a2-110">Before you begin</span></span>

* <span data-ttu-id="b02a2-111">De conversie vereist een herstart van de virtuele machine, zodat de migratie van de opslag van uw schijven tijdens een onderhoudsvenster vooraf bestaande plannen.</span><span class="sxs-lookup"><span data-stu-id="b02a2-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="b02a2-112">Als u niet-beheerde schijven eerst [converteren naar beheerde schijven](convert-unmanaged-to-managed-disks.md) in dit artikel gebruiken om over te schakelen tussen de twee opties voor opslag.</span><span class="sxs-lookup"><span data-stu-id="b02a2-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="b02a2-113">Standaard alle beheerde schijven van een virtuele machine converteren naar premium, en omgekeerd</span><span class="sxs-lookup"><span data-stu-id="b02a2-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="b02a2-114">In het volgende voorbeeld laten we zien hoe overschakelen van de schijven van een virtuele machine van standaard naar premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b02a2-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="b02a2-115">U kunt beheerde premium-schijven, uw virtuele machine gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b02a2-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="b02a2-116">In dit voorbeeld wordt ook verandert in een grootte die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b02a2-116">This example also switches to a size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains the virtual machine
rgName='yourResourceGroup'

#Name of the virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard to premium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate the VM before changing the size of the VM
az vm deallocate --name $vmName --resource-group $rgName

#Change the VM size to a size that supports premium storage 
#Skip this step if converting storage from premium to standard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update the sku of all the data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update the sku of the OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="b02a2-117">Een beheerde schijf van standard converteren naar premium, en omgekeerd</span><span class="sxs-lookup"><span data-stu-id="b02a2-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="b02a2-118">Voor uw workload ontwikkelen en testen, is het raadzaam combinatie van standard en premium-schijven voor uw kosten hebben.</span><span class="sxs-lookup"><span data-stu-id="b02a2-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="b02a2-119">U kunt dit doen door te upgraden naar de premium-opslag alleen op de schijven die betere prestaties zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="b02a2-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="b02a2-120">In het volgende voorbeeld laten we zien hoe overschakelen van één schijf van een virtuele machine van standaard naar premium-opslag, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="b02a2-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="b02a2-121">U kunt beheerde premium-schijven, uw virtuele machine gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b02a2-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="b02a2-122">In dit voorbeeld wordt ook verandert in een grootte die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b02a2-122">This example also switches to a size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains the managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard to premium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get the parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate the VM before changing the size of the VM
az vm deallocate --ids $vmId 

#Change the VM size to a size that supports premium storage 
#Skip this step if converting storage from premium to standard
az vm resize --ids $vmId --size $size

# Update the sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="b02a2-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b02a2-123">Next steps</span></span>

<span data-ttu-id="b02a2-124">Een alleen-lezen kopie van een virtuele machine uitvoeren met behulp van [momentopnamen](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="b02a2-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

