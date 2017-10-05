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
# <a name="increase-the-size-of-a-data-disk-attached-to-a-windows-vm"></a><span data-ttu-id="5f833-103">Verhoog de grootte van een gegevensschijf gekoppeld aan een Windows-VM</span><span class="sxs-lookup"><span data-stu-id="5f833-103">Increase the size of a data disk attached to a Windows VM</span></span>

<span data-ttu-id="5f833-104">Als u de grootte van de gegevensschijf gekoppeld aan uw virtuele machine vergroten wilt, kunt u de grootte die met behulp van PowerShell verhogen.</span><span class="sxs-lookup"><span data-stu-id="5f833-104">If you need to increase the size of the data disk attached to your virtual machine, you can increase the size using PowerShell.</span></span> <span data-ttu-id="5f833-105">Nadat u de grootte van de gegevensschijf in de instellingen voor virtuele machine van Azure verhoogt, moet u ook de nieuwe schijfruimte in de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5f833-105">After you increase the size of the data disk in the Azure VM settings, you also need to allocate the new disk space within the VM.</span></span>


## <a name="use-powershell-to-increase-the-size-of-a-managed-data-disk"></a><span data-ttu-id="5f833-106">Gebruik Powershell om de grootte van een beheerde gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="5f833-106">Use Powershell to increase the size of a managed data disk</span></span>

<span data-ttu-id="5f833-107">Gebruik de volgende PowerShell-cmdlets voor een verhoging van de grootte van de schijf van een beheerd gegevens:</span><span class="sxs-lookup"><span data-stu-id="5f833-107">To increase the size of a managed data disk, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="5f833-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f833-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="5f833-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5f833-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="5f833-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5f833-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="5f833-111">Update AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="5f833-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="5f833-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5f833-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="5f833-113">Het volgende script begeleidt u bij het ophalen van de VM-gegevens, te selecteren van de gegevensschijf en geven de nieuwe grootte.</span><span class="sxs-lookup"><span data-stu-id="5f833-113">The following script will walk you through getting the VM information, selecting the data disk and specifying the new size.</span></span>

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

## <a name="use-powershell-to-increase-the-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="5f833-114">Gebruik PowerShell om de grootte van de gegevensschijf van een niet-beheerde</span><span class="sxs-lookup"><span data-stu-id="5f833-114">Use PowerShell to increase the size of an unmanaged data disk</span></span>

<span data-ttu-id="5f833-115">Gebruik de volgende PowerShell-cmdlets voor een verhoging van de grootte van niet-beheerde gegevensschijven in een opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="5f833-115">To increase the size of unmanaged data disks in a storage account, use the following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="5f833-116">Get AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="5f833-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="5f833-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5f833-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="5f833-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="5f833-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="5f833-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="5f833-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="5f833-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5f833-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="5f833-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5f833-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="5f833-122">Het volgende script helpt u bij het ophalen van de virtuele machine en opslag accountgegevens, de gegevensschijf selecteren en de nieuwe grootte op te geven.</span><span class="sxs-lookup"><span data-stu-id="5f833-122">The following script will walk you through getting the VM and storage account information, selecting the data disk and specifying the new size.</span></span>

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

## <a name="allocate-the-unallocated-disk-space"></a><span data-ttu-id="5f833-123">De niet-toegewezen schijfruimte toewijzen</span><span class="sxs-lookup"><span data-stu-id="5f833-123">Allocate the unallocated disk space</span></span>

<span data-ttu-id="5f833-124">Nadat u hebt de schijf groter is aangebracht, moet u de nieuwe niet-toegewezen ruimte uit vanuit de virtuele machine toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="5f833-124">Once you have made the drive larger, you need to allocate the new unallocated space from within the VM.</span></span> <span data-ttu-id="5f833-125">Als u wilt de ruimte toewijzen, kunt u verbinding met het VM-Gebruik Schijfbeheer (diskmgmt.msc).</span><span class="sxs-lookup"><span data-stu-id="5f833-125">To allocate the space, you can connect to the VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="5f833-126">Of als u WinRM en een certificaat op de virtuele machine ingeschakeld wanneer u het hebt gemaakt, kunt u extern PowerShell Initialiseer de schijf.</span><span class="sxs-lookup"><span data-stu-id="5f833-126">Or, if you enabled WinRM and a certificate on the VM when you created it, you can use remote PowerShell to initialize the disk.</span></span> <span data-ttu-id="5f833-127">U kunt ook een extensie voor aangepaste scripts gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5f833-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="5f833-128">Het scriptbestand bevatten dat lijkt op deze code naar het station toewijzen aan de maximale grootte verhogen de schijven:</span><span class="sxs-lookup"><span data-stu-id="5f833-128">The script file can contain something like this code to increase the drive allocation to the maximum size the disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="5f833-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f833-129">Next Steps</span></span>
- [<span data-ttu-id="5f833-130">Meer informatie over schijven en VHD 's</span><span class="sxs-lookup"><span data-stu-id="5f833-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
