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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Converteren van Azure storage schijven beheerd van standaard toopremium, en vice versa

Beheerde schijven biedt twee opties voor opslag: [Premium](../../storage/storage-premium-storage.md) (SSD-gebaseerde) en [standaard](../../storage/storage-standard-storage.md) (gebaseerd op harde schijf). Hiermee kunt u tooeasily schakelen tussen Hallo twee opties met minimale downtime op basis van uw prestatievereisten past. Deze mogelijkheid is niet beschikbaar voor niet-beheerde schijven. Maar u kunt eenvoudig [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) tooeasily schakelen tussen Hallo twee opties.

Dit artikel laat zien hoe tooconvert schijven die worden beheerd vanaf standaard toopremium, en vice versa met behulp van Azure PowerShell. Als u tooinstall moet of een upgrade uitvoeren, Zie [installeren en configureren van Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Voordat u begint

* Hallo conversie vereist Hallo VM opnieuw wordt opgestart, dus plannen Hallo-migratie van de opslag van uw schijven tijdens een vooraf bestaande onderhoudsvenster. 
* Als u niet-beheerde schijven eerst [toomanaged schijven geconverteerd](convert-unmanaged-to-managed-disks.md) toouse in dit artikel tooswitch tussen twee Hallo opslagopties. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Converteert alle Hallo beheerd schijven van een virtuele machine van de standaard toopremium, en vice versa

In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch alle schijven van een virtuele machine uit de opslag van de standaard toopremium Hallo. premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag. In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Een beheerde schijf converteren van standaard toopremium, en vice versa

Voor uw workload ontwikkelen en testen kunt u toohave combinatie van standard en premium-schijven tooreduce uw kosten. U kunt dit doen door het upgraden van toopremium opslag, alleen Hallo-schijven die betere prestaties zijn vereist. In de Hallo voorbeeld te volgen, laten we zien hoe tooswitch één schijf van een virtuele machine uit de standaard toopremium opslag, en vice versa. premium toouse schijven die worden beheerd, uw virtuele machine moet gebruiken een [VM-grootte](sizes.md) die ondersteuning biedt voor premium-opslag. In dit voorbeeld wordt ook tooa grootte die ondersteuning biedt voor premium-opslag.

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

## <a name="next-steps"></a>Volgende stappen

Een alleen-lezen kopie van een virtuele machine uitvoeren met behulp van [momentopnamen](snapshot-copy-managed-disk.md).

