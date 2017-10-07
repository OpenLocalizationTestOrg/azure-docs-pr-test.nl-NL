---
title: aaaExpand een gegevensschijf gekoppeld tooa Windows virtuele machine in Azure | Microsoft Docs
description: Vouw Hallo grootte van een gegevensschijf die is aangesloten tooa Windows virtuele machine met behulp van PowerShell.
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a>Verhoging van het Hallo-grootte van een gegevensschijf gekoppeld tooa Windows VM

Als u tooincrease Hallo grootte van Hallo gegevens schijf is gekoppeld aan tooyour virtuele machine nodig hebt, kunt u vergroten Hallo met behulp van PowerShell. Nadat u Hallo Hallo gegevensschijf in hello Azure VM-instellingen tekengrootte, moet u ook tooallocate Hallo nieuwe schijfruimte vrij binnen Hallo VM.


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a>Gebruik Powershell tooincrease Hallo grootte van een beheerde gegevensschijf

tooincrease hello grootte van een beheerde gegevensschijf gebruik Hallo PowerShell-cmdlets te volgen:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [Update AzureRmDisk](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

Hallo begeleidt volgende script u bij het ophalen van informatie over het Hallo-VM, Hallo gegevensschijf selecteren en Hallo nieuwe grootte opgeven.

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a>Gebruik PowerShell tooincrease Hallo grootte van de gegevensschijf van een niet-beheerde

tooincrease hello grootte van niet-beheerde gegevensschijven in een opslagaccount, gebruik Hallo PowerShell-cmdlets te volgen:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

Hallo begeleidt volgende script u bij Hallo virtuele machine en opslag accountgegevens ophalen, Hallo gegevensschijf selecteren en Hallo nieuwe grootte opgeven.

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a>Hallo niet-toegewezen schijfruimte toewijzen

Nadat u Hallo station groter gemaakt hebt, moet u tooallocate Hallo nieuwe vrije ruimte van binnen Hallo VM. tooallocate hello ruimte, kunt u toohello VM Gebruik Schijfbeheer (diskmgmt.msc). Of als u de WinRM- en een certificaat op Hallo VM ingeschakeld wanneer u het hebt gemaakt, kunt u extern PowerShell tooinitialize Hallo schijf. U kunt ook een extensie voor aangepaste scripts gebruiken:

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

Hallo-scriptbestand kan bevatten dat lijkt op deze code tooincrease Hallo station toewijzing toohello maximumgrootte Hallo schijven:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Volgende stappen
- [Meer informatie over schijven en VHD 's](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
