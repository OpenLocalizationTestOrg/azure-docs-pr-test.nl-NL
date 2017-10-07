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
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="cfa4e-103">Verhoging van het Hallo-grootte van een gegevensschijf gekoppeld tooa Windows VM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="cfa4e-104">Als u tooincrease Hallo grootte van Hallo gegevens schijf is gekoppeld aan tooyour virtuele machine nodig hebt, kunt u vergroten Hallo met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfa4e-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="cfa4e-105">Nadat u Hallo Hallo gegevensschijf in hello Azure VM-instellingen tekengrootte, moet u ook tooallocate Hallo nieuwe schijfruimte vrij binnen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="cfa4e-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="cfa4e-106">Gebruik Powershell tooincrease Hallo grootte van een beheerde gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="cfa4e-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="cfa4e-107">tooincrease hello grootte van een beheerde gegevensschijf gebruik Hallo PowerShell-cmdlets te volgen:</span><span class="sxs-lookup"><span data-stu-id="cfa4e-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="cfa4e-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="cfa4e-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="cfa4e-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="cfa4e-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="cfa4e-111">Update AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="cfa4e-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="cfa4e-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="cfa4e-113">Hallo begeleidt volgende script u bij het ophalen van informatie over het Hallo-VM, Hallo gegevensschijf selecteren en Hallo nieuwe grootte opgeven.</span><span class="sxs-lookup"><span data-stu-id="cfa4e-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

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

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="cfa4e-114">Gebruik PowerShell tooincrease Hallo grootte van de gegevensschijf van een niet-beheerde</span><span class="sxs-lookup"><span data-stu-id="cfa4e-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="cfa4e-115">tooincrease hello grootte van niet-beheerde gegevensschijven in een opslagaccount, gebruik Hallo PowerShell-cmdlets te volgen:</span><span class="sxs-lookup"><span data-stu-id="cfa4e-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="cfa4e-116">Get AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="cfa4e-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="cfa4e-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="cfa4e-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="cfa4e-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="cfa4e-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="cfa4e-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="cfa4e-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cfa4e-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="cfa4e-122">Hallo begeleidt volgende script u bij Hallo virtuele machine en opslag accountgegevens ophalen, Hallo gegevensschijf selecteren en Hallo nieuwe grootte opgeven.</span><span class="sxs-lookup"><span data-stu-id="cfa4e-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

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

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="cfa4e-123">Hallo niet-toegewezen schijfruimte toewijzen</span><span class="sxs-lookup"><span data-stu-id="cfa4e-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="cfa4e-124">Nadat u Hallo station groter gemaakt hebt, moet u tooallocate Hallo nieuwe vrije ruimte van binnen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="cfa4e-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="cfa4e-125">tooallocate hello ruimte, kunt u toohello VM Gebruik Schijfbeheer (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="cfa4e-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="cfa4e-126">Of als u de WinRM- en een certificaat op Hallo VM ingeschakeld wanneer u het hebt gemaakt, kunt u extern PowerShell tooinitialize Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="cfa4e-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="cfa4e-127">U kunt ook een extensie voor aangepaste scripts gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cfa4e-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="cfa4e-128">Hallo-scriptbestand kan bevatten dat lijkt op deze code tooincrease Hallo station toewijzing toohello maximumgrootte Hallo schijven:</span><span class="sxs-lookup"><span data-stu-id="cfa4e-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="cfa4e-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cfa4e-129">Next Steps</span></span>
- [<span data-ttu-id="cfa4e-130">Meer informatie over schijven en VHD 's</span><span class="sxs-lookup"><span data-stu-id="cfa4e-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
