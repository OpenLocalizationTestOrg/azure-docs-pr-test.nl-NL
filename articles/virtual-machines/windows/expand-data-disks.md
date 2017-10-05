---
title: Vouw een gegevensschijf gekoppeld aan een Windows-VM in Azure | Microsoft Docs
description: Vouw de grootte van een gegevensschijf die is gekoppeld aan een virtuele Windows-machine met behulp van PowerShell.
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
ms.openlocfilehash: 5529856c2ffcd2942fe3fc2b438f7e3fd16a67b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a>Verhoog de grootte van een gegevensschijf gekoppeld aan een Windows-VM

Als u de grootte van de gegevensschijf gekoppeld aan uw virtuele machine vergroten wilt, kunt u de grootte die met behulp van PowerShell verhogen. Nadat u de grootte van de gegevensschijf in de instellingen voor virtuele machine van Azure verhoogt, moet u ook de nieuwe schijfruimte in de virtuele machine.


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a>Gebruik Powershell om de grootte van een beheerde gegevensschijf

Gebruik de volgende PowerShell-cmdlets voor een verhoging van de grootte van de schijf van een beheerd gegevens:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get-AzureRMReseourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                        | [Update AzureRmDisk](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

Het volgende script begeleidt u bij het ophalen van de VM-gegevens, te selecteren van de gegevensschijf en geven de nieuwe grootte.

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select the resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for the data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update the configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start the VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a>Gebruik PowerShell om de grootte van de gegevensschijf van een niet-beheerde

Gebruik de volgende PowerShell-cmdlets voor een verhoging van de grootte van niet-beheerde gegevensschijven in een opslagaccount:

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [Get AzureRMStorageAccount](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [Stop-AzureRMVM](/powershell/module/azurerm.compute/stop-azurermvm)                       | [Set-AzureRmVMDataDisk](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm)                   | [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

Het volgende script helpt u bij het ophalen van de virtuele machine en opslag accountgegevens, de gegevensschijf selecteren en de nieuwe grootte op te geven.

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select the VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk to resize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk to resize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior to resizing data disk

    $vm | Stop-AzureRMVM -Force

# Set the new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update the configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start the VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-the-unallocated-disk-space"></a>De niet-toegewezen schijfruimte toewijzen

Nadat u hebt de schijf groter is aangebracht, moet u de nieuwe niet-toegewezen ruimte uit vanuit de virtuele machine toe te wijzen. Als u wilt de ruimte toewijzen, kunt u verbinding met het VM-Gebruik Schijfbeheer (diskmgmt.msc). Of als u WinRM en een certificaat op de virtuele machine ingeschakeld wanneer u het hebt gemaakt, kunt u extern PowerShell Initialiseer de schijf. U kunt ook een extensie voor aangepaste scripts gebruiken:

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

Het scriptbestand bevatten dat lijkt op deze code naar het station toewijzen aan de maximale grootte verhogen de schijven:

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a>Volgende stappen
- [Meer informatie over schijven en VHD 's](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
