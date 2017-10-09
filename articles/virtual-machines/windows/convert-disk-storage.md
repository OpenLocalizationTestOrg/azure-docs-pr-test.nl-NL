---
title: aaaConvert Azure beheerd schijven opslag van standaard toopremium, en vice versa | Microsoft Docs
description: Hoe tooconvert Azure schijven die worden beheerd vanaf standaard toopremium en omgekeerd, met behulp van Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="1e382-103">Converteren van Azure storage schijven beheerd van standaard toopremium, en vice versa</span><span class="sxs-lookup"><span data-stu-id="1e382-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="1e382-104">Beheerde schijven biedt twee opties voor opslag: [Premium](../../storage/storage-premium-storage.md) (SSD-gebaseerde) en [standaard](../../storage/storage-standard-storage.md) (gebaseerd op harde schijf).</span><span class="sxs-lookup"><span data-stu-id="1e382-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="1e382-105">Hiermee kunt u tooeasily schakelen tussen Hallo twee opties met minimale downtime op basis van uw prestatievereisten past.</span><span class="sxs-lookup"><span data-stu-id="1e382-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="1e382-106">Deze mogelijkheid is niet beschikbaar voor niet-beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="1e382-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="1e382-107">Maar u kunt eenvoudig [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) tooeasily schakelen tussen Hallo twee opties.</span><span class="sxs-lookup"><span data-stu-id="1e382-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="1e382-108">Dit artikel laat zien hoe tooconvert schijven die worden beheerd vanaf standaard toopremium, en vice versa met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e382-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="1e382-109">Als u tooinstall moet of een upgrade uitvoeren, Zie [installeren en configureren van Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1e382-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e382-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="1e382-110">Before you begin</span></span>

* <span data-ttu-id="1e382-111">Hallo conversie vereist Hallo VM opnieuw wordt opgestart, dus plannen Hallo-migratie van de opslag van uw schijven tijdens een vooraf bestaande onderhoudsvenster.</span><span class="sxs-lookup"><span data-stu-id="1e382-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="1e382-112">Als u niet-beheerde schijven eerst [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) toouse in dit artikel tooswitch tussen twee Hallo opslagopties.</span><span class="sxs-lookup"><span data-stu-id="1e382-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="1e382-113">Converteert alle Hallo beheerd schijven van een virtuele machine van de standaard toopremium, en vice versa</span><span class="sxs-lookup"><span data-stu-id="1e382-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="1e382-114">In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch alle schijven van een virtuele machine uit de opslag van de standaard toopremium Hallo.</span><span class="sxs-lookup"><span data-stu-id="1e382-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="1e382-115">premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1e382-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="1e382-116">In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1e382-116">This example also switches tooa size that supports premium storage.</span></span>

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="1e382-117">Een beheerde schijf converteren van standaard toopremium, en vice versa</span><span class="sxs-lookup"><span data-stu-id="1e382-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="1e382-118">Voor uw workload ontwikkelen en testen kunt u toohave combinatie van standard en premium-schijven tooreduce uw kosten.</span><span class="sxs-lookup"><span data-stu-id="1e382-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="1e382-119">U kunt dit doen door het upgraden van toopremium opslag, alleen Hallo-schijven die betere prestaties zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="1e382-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="1e382-120">In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch één schijf van een virtuele machine uit de standaard toopremium opslag, en vice versa.</span><span class="sxs-lookup"><span data-stu-id="1e382-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="1e382-121">premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1e382-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="1e382-122">In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="1e382-122">This example also switches tooa size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="1e382-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e382-123">Next steps</span></span>

<span data-ttu-id="1e382-124">Een alleen-lezen kopie van een virtuele machine uitvoeren met behulp van [momentopnamen](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1e382-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

