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
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="b58d3-103">Koppelen van een schijf tooa voor gegevens virtuele machine van Windows met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b58d3-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="b58d3-104">Dit artikel laat zien hoe tooattach zowel nieuwe als bestaande schijven tooa Windows virtuele machine met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b58d3-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="b58d3-105">Als uw VM beheerde schijven gebruikt, kunt u extra beheerde gegevensschijven koppelen.</span><span class="sxs-lookup"><span data-stu-id="b58d3-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="b58d3-106">Ook kunt u gegevens van niet-beheerde schijven tooa VM die gebruikmaakt van niet-beheerde schijven in een storage-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="b58d3-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="b58d3-107">Voordat u dit doet, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="b58d3-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="b58d3-108">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="b58d3-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="b58d3-109">Zie voor meer informatie [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b58d3-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="b58d3-110">Premium-opslag toouse, moet u een Premium-opslag ingeschakeld VM-grootte zoals Hallo DS-serie- of GS-serie virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b58d3-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="b58d3-111">Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="b58d3-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="b58d3-112">Premium-opslag is beschikbaar in bepaalde regio's.</span><span class="sxs-lookup"><span data-stu-id="b58d3-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="b58d3-113">Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b58d3-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b58d3-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="b58d3-114">Before you begin</span></span>
<span data-ttu-id="b58d3-115">Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="b58d3-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b58d3-116">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="b58d3-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b58d3-117">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b58d3-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="b58d3-118">Een leeg gegevens schijf tooa virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="b58d3-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="b58d3-119">Dit voorbeeld toont hoe tooadd gegevens in een lege schijf tooan bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b58d3-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="b58d3-120">Beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="b58d3-120">Using managed disks</span></span>

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

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="b58d3-121">Gebruik van niet-beheerde schijven in een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="b58d3-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="b58d3-122">Hallo schijf initialiseren</span><span class="sxs-lookup"><span data-stu-id="b58d3-122">Initialize hello disk</span></span>

<span data-ttu-id="b58d3-123">Nadat u een lege schijf toevoegt, moet u tooinitialize deze.</span><span class="sxs-lookup"><span data-stu-id="b58d3-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="b58d3-124">tooinitialize hello schijf, u kunt aanmelden tooa virtuele machine en Gebruik Schijfbeheer.</span><span class="sxs-lookup"><span data-stu-id="b58d3-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="b58d3-125">Als u de WinRM- en een certificaat op Hallo VM ingeschakeld wanneer u het hebt gemaakt, kunt u extern PowerShell tooinitialize Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="b58d3-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="b58d3-126">U kunt ook een extensie voor aangepaste scripts gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b58d3-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="b58d3-127">Hallo-scriptbestand kan bevatten dat lijkt op deze code tooinitialize Hallo schijven:</span><span class="sxs-lookup"><span data-stu-id="b58d3-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

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


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="b58d3-128">Een bestaande gegevens schijf tooa VM koppelen</span><span class="sxs-lookup"><span data-stu-id="b58d3-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="b58d3-129">U kunt ook een bestaande VHD koppelen als een beheerde gegevens schijf tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b58d3-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="b58d3-130">Beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="b58d3-130">Using managed disks</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b58d3-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b58d3-131">Next steps</span></span>

<span data-ttu-id="b58d3-132">Maak een [momentopname](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="b58d3-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
