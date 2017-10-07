---
title: aaaAttach een gegevens schijf tooa virtuele Windows-machine in Azure met behulp van PowerShell | Microsoft Docs
description: Hoe tooattach nieuwe of bestaande gegevens schijf tooa virtuele machine van Windows PowerShell gebruiken met Resource Manager-implementatiemodel Hallo.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>Koppelen van een schijf tooa voor gegevens virtuele machine van Windows met behulp van PowerShell

Dit artikel laat zien hoe tooattach zowel nieuwe als bestaande schijven tooa Windows virtuele machine met behulp van PowerShell. Als uw VM beheerde schijven gebruikt, kunt u extra beheerde gegevensschijven koppelen. Ook kunt u gegevens van niet-beheerde schijven tooa VM die gebruikmaakt van niet-beheerde schijven in een storage-account koppelen.

Voordat u dit doet, controleert u de volgende tips:
* Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Premium-opslag toouse, moet u een Premium-opslag ingeschakeld VM-grootte zoals Hallo DS-serie- of GS-serie virtuele machine. Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts. Premium-opslag is beschikbaar in bepaalde regio's. Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="before-you-begin"></a>Voordat u begint
Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. Voer Hallo na de opdracht tooinstall deze.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>Een leeg gegevens schijf tooa virtuele machine toevoegen

Dit voorbeeld toont hoe tooadd gegevens in een lege schijf tooan bestaande virtuele machine.

### <a name="using-managed-disks"></a>Beheerde schijven

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a>Gebruik van niet-beheerde schijven in een opslagaccount

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>Hallo schijf initialiseren

Nadat u een lege schijf toevoegt, moet u tooinitialize deze. tooinitialize hello schijf, u kunt aanmelden tooa virtuele machine en Gebruik Schijfbeheer. Als u de WinRM- en een certificaat op Hallo VM ingeschakeld wanneer u het hebt gemaakt, kunt u extern PowerShell tooinitialize Hallo schijf. U kunt ook een extensie voor aangepaste scripts gebruiken: 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
Hallo-scriptbestand kan bevatten dat lijkt op deze code tooinitialize Hallo schijven:

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a>Een bestaande gegevens schijf tooa VM koppelen

U kunt ook een bestaande VHD koppelen als een beheerde gegevens schijf tooa virtuele machine. 

### <a name="using-managed-disks"></a>Beheerde schijven

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>Volgende stappen

Maak een [momentopname](snapshot-copy-managed-disk.md).
