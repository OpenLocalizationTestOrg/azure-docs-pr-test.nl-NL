---
title: aaaConvert Azure beheerd schijven opslag van standaard toopremium, en vice versa | Microsoft Docs
description: Hoe beheerd tooconvert Azure storage van de schijven van standaard toopremium en omgekeerd, met behulp van Azure CLI.
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
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="b8fe6-103">Converteren van Azure storage schijven beheerd van standaard toopremium, en vice versa</span><span class="sxs-lookup"><span data-stu-id="b8fe6-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="b8fe6-104">Beheerde schijven biedt twee opties voor opslag: [Premium](../../storage/storage-premium-storage.md) (SSD-gebaseerde) en [standaard](../../storage/storage-standard-storage.md) (gebaseerd op harde schijf).</span><span class="sxs-lookup"><span data-stu-id="b8fe6-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="b8fe6-105">Hiermee kunt u tooeasily schakelen tussen Hallo twee opties met minimale downtime op basis van uw prestatievereisten past.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="b8fe6-106">Deze mogelijkheid is niet beschikbaar voor niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="b8fe6-107">Maar u kunt eenvoudig [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) tooeasily schakelen tussen Hallo twee opties.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="b8fe6-108">Dit artikel laat zien hoe tooconvert schijven die worden beheerd vanaf standaard toopremium, en vice versa met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="b8fe6-109">Als u tooinstall moet of een upgrade uitvoeren, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b8fe6-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b8fe6-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b8fe6-110">Before you begin</span></span>

* <span data-ttu-id="b8fe6-111">Hallo conversie vereist Hallo VM opnieuw wordt opgestart, dus plannen Hallo-migratie van de opslag van uw schijven tijdens een vooraf bestaande onderhoudsvenster.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="b8fe6-112">Als u niet-beheerde schijven eerst [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) toouse in dit artikel tooswitch tussen twee Hallo opslagopties.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="b8fe6-113">Converteert alle Hallo beheerd schijven van een virtuele machine van de standaard toopremium, en vice versa</span><span class="sxs-lookup"><span data-stu-id="b8fe6-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="b8fe6-114">In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch alle schijven van een virtuele machine uit de opslag van de standaard toopremium Hallo.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="b8fe6-115">premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="b8fe6-116">In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-116">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="b8fe6-117">Een beheerde schijf converteren van standaard toopremium, en vice versa</span><span class="sxs-lookup"><span data-stu-id="b8fe6-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="b8fe6-118">Voor uw workload ontwikkelen en testen kunt u toohave combinatie van standard en premium-schijven tooreduce uw kosten.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="b8fe6-119">U kunt dit doen door het upgraden van toopremium opslag, alleen Hallo-schijven die betere prestaties zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="b8fe6-120">In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch één schijf van een virtuele machine uit de standaard toopremium opslag, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="b8fe6-121">premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="b8fe6-122">In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="b8fe6-122">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="b8fe6-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8fe6-123">Next steps</span></span>

<span data-ttu-id="b8fe6-124">Een alleen-lezen kopie van een virtuele machine uitvoeren met behulp van [momentopnamen](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="b8fe6-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

