---
title: een Windows-VM vanaf een speciale VHD in Azure aaaCreate | Microsoft Docs
description: Een nieuwe Windows VM maken door het koppelen van een gespecialiseerde beheerde schijf als besturingssysteemschijf Hallo met Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="34ec6-103">Een virtuele Windows-machine maken van een gespecialiseerde schijf</span><span class="sxs-lookup"><span data-stu-id="34ec6-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="34ec6-104">Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde beheerde schijf als Hallo besturingssysteemschijf met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="34ec6-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="34ec6-105">Een speciale schijf is een kopie van de virtuele harde schijf (VHD) van een bestaande virtuele machine die wordt onderhouden door Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="34ec6-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="34ec6-106">Wanneer u een speciale VHD toocreate een nieuwe virtuele machine, Hallo Hallo nieuwe virtuele machine behoudt Hallo computernaam van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="34ec6-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="34ec6-107">Andere computer-specifieke informatie wordt ook opgeslagen en in sommige gevallen kan deze dubbele gegevens problemen kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="34ec6-108">Zich bewust zijn van welke typen computerspecifieke informatie uw toepassingen afhankelijk zijn van bij het kopiëren van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34ec6-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="34ec6-109">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="34ec6-109">You have two options:</span></span>
* [<span data-ttu-id="34ec6-110">Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="34ec6-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="34ec6-111">Kopiëren van een bestaande virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="34ec6-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="34ec6-112">Dit onderwerp leest u hoe toouse schijven die worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="34ec6-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="34ec6-113">Als u een verouderde implementatie hebt waarvoor een opslagaccount gebruikt, Zie [een virtuele machine vanaf een speciale VHD in een opslagaccount maken](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="34ec6-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="34ec6-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="34ec6-114">Before you begin</span></span>
<span data-ttu-id="34ec6-115">Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="34ec6-116">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34ec6-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="34ec6-117">Optie 1: Een gespecialiseerde VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="34ec6-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="34ec6-118">U kunt VHD van een speciale virtuele machine met een lokale virtualisatie hulpprogramma gemaakt, zoals Hyper-V of een virtuele machine die zijn geëxporteerd uit een andere cloud Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="34ec6-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="34ec6-119">Hallo VM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="34ec6-119">Prepare hello VM</span></span>
<span data-ttu-id="34ec6-120">Als u van plan toouse bent Hallo VHD-toocreate is een nieuwe virtuele machine, Controleer Hallo stappen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="34ec6-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="34ec6-121">[Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34ec6-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="34ec6-122">**Geen** generalize Hallo van virtuele machine met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="34ec6-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="34ec6-123">Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op Hallo VM (zoals VMware tools).</span><span class="sxs-lookup"><span data-stu-id="34ec6-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="34ec6-124">Zorg ervoor dat Hallo VM geconfigureerde toopull is het IP-adres en DNS-instellingen via DHCP.</span><span class="sxs-lookup"><span data-stu-id="34ec6-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="34ec6-125">Dit zorgt ervoor dat Hallo-server verkrijgt IP-adres binnen Hallo VNet wanneer deze opgestart wordt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="34ec6-126">Hallo storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="34ec6-126">Get hello storage account</span></span>
<span data-ttu-id="34ec6-127">U moet een opslag-account in Azure toostore Hallo VHD geüpload.</span><span class="sxs-lookup"><span data-stu-id="34ec6-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="34ec6-128">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="34ec6-129">tooshow hello beschikbaar storage-accounts, typt u:</span><span class="sxs-lookup"><span data-stu-id="34ec6-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="34ec6-130">Als u een bestaand opslagaccount toouse wilt, gaat u verder toohello [uploaden Hallo VHD](#upload-the-vhd-to-your-storage-account) sectie.</span><span class="sxs-lookup"><span data-stu-id="34ec6-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="34ec6-131">Als u een opslagaccount toocreate moet, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="34ec6-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="34ec6-132">U moet Hallo-naam van resourcegroep Hallo waar Hallo storage-account moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="34ec6-133">toofind uit alle Hallo resourcegroepen in uw abonnement, type:</span><span class="sxs-lookup"><span data-stu-id="34ec6-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="34ec6-134">een resourcegroep met de naam toocreate *myResourceGroup* in Hallo *VS-West* regio, type:</span><span class="sxs-lookup"><span data-stu-id="34ec6-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="34ec6-135">Maken van een opslagaccount met de naam *mystorageaccount* in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="34ec6-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="34ec6-136">Hallo VHD tooyour storage-account uploaden</span><span class="sxs-lookup"><span data-stu-id="34ec6-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="34ec6-137">Gebruik Hallo [toevoegen AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Hallo VHD tooa container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="34ec6-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="34ec6-138">In dit voorbeeld uploads Hallo bestand *myVHD.vhd* van `"C:\Users\Public\Documents\Virtual hard disks\"` tooa opslagaccount met de naam *mystorageaccount* in Hallo *myResourceGroup* resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="34ec6-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="34ec6-139">Hallo-bestand wordt opgeslagen in het Hallo-container met de naam *mycontainer* en worden nieuwe bestandsnaam Hallo *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="34ec6-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="34ec6-140">Als dit lukt, kunt u een antwoord dat vergelijkbare toothis lijkt krijgen:</span><span class="sxs-lookup"><span data-stu-id="34ec6-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="34ec6-141">Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete</span><span class="sxs-lookup"><span data-stu-id="34ec6-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="34ec6-142">Een beheerde schijf van Hallo VHD maken</span><span class="sxs-lookup"><span data-stu-id="34ec6-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="34ec6-143">Maken van een beheerde schijf vanuit Hallo VHD in uw storage-account met gespecialiseerde [nieuw AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="34ec6-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="34ec6-144">In dit voorbeeld wordt **myOSDisk1** voor schijfnaam hello, Hallo puts schijf in *StandardLRS* opslag en maakt gebruik van *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* zoals hello URI voor Hallo bron VHD.</span><span class="sxs-lookup"><span data-stu-id="34ec6-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="34ec6-145">Maak een nieuwe resourcegroep voor Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34ec6-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="34ec6-146">Maken van nieuwe OS-schijf Hallo van Hallo VHD geüpload.</span><span class="sxs-lookup"><span data-stu-id="34ec6-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="34ec6-147">Optie 2: Een bestaande virtuele machine van Azure kopiëren</span><span class="sxs-lookup"><span data-stu-id="34ec6-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="34ec6-148">U kunt een kopie van een virtuele machine dat maakt gebruik van schijven die worden beheerd door het maken van een momentopname van Hallo VM vervolgens met die toocreate momentopname van een nieuwe schijf- en een nieuwe virtuele machine beheerde maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="34ec6-149">Een momentopname van de besturingssysteemschijf Hallo</span><span class="sxs-lookup"><span data-stu-id="34ec6-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="34ec6-150">U kunt nemen een momentopname van en volledige virtuele machine (inclusief alle schijven) of van één schijf.</span><span class="sxs-lookup"><span data-stu-id="34ec6-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="34ec6-151">Hallo volgende stappen ziet u hoe een momentopname van NET Hallo OS schijf van het gebruik van uw VM tootake Hallo [nieuw AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34ec6-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="34ec6-152">Sommige parameters instellen.</span><span class="sxs-lookup"><span data-stu-id="34ec6-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="34ec6-153">Hallo VM-object ophalen.</span><span class="sxs-lookup"><span data-stu-id="34ec6-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="34ec6-154">De naam van de schijf Hallo OS ophalen.</span><span class="sxs-lookup"><span data-stu-id="34ec6-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="34ec6-155">Hallo momentopname configuratie maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="34ec6-156">Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="34ec6-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="34ec6-157">Als u van plan toouse Hallo momentopname toocreate een virtuele machine die behoeften toobe hoge prestaties bent, gebruikt u Hallo parameter `-AccountType Premium_LRS` met Hallo nieuw AzureRmSnapshot-opdracht.</span><span class="sxs-lookup"><span data-stu-id="34ec6-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="34ec6-158">Hallo-parameter wordt Hallo momentopname gemaakt, zodat deze wordt opgeslagen als een schijf Premium beheerd.</span><span class="sxs-lookup"><span data-stu-id="34ec6-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="34ec6-159">Premium-schijven beheerd zijn duurder dan de standaard.</span><span class="sxs-lookup"><span data-stu-id="34ec6-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="34ec6-160">Dus wees zeker dat u echt Premium voordat u de parameter Hallo nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="34ec6-161">Een nieuwe schijf maken vanuit een momentopname Hallo</span><span class="sxs-lookup"><span data-stu-id="34ec6-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="34ec6-162">Maak een beheerde schijf van Hallo momentopname over met [nieuw AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="34ec6-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="34ec6-163">In dit voorbeeld wordt *myOSDisk* voor de naam van de schijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="34ec6-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="34ec6-164">Maak een nieuwe resourcegroep voor Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34ec6-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="34ec6-165">De naam van de schijf Hallo OS ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34ec6-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="34ec6-166">Hallo-beheerde schijven maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="34ec6-167">Maken van nieuwe virtuele machine Hallo</span><span class="sxs-lookup"><span data-stu-id="34ec6-167">Create hello new VM</span></span> 

<span data-ttu-id="34ec6-168">Maken van netwerken en andere VM-resources toobe die wordt gebruikt door Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34ec6-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="34ec6-169">Hallo-subNet en een vNet maken</span><span class="sxs-lookup"><span data-stu-id="34ec6-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="34ec6-170">Hallo vNet en subNet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34ec6-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="34ec6-171">Hallo subNet maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-171">Create hello subNet.</span></span> <span data-ttu-id="34ec6-172">In dit voorbeeld wordt een subnet met de naam **mySubNet**, in de resourcegroep Hallo **myDestinationResourceGroup**, en stelt Hallo adresvoorvoegsel subnet te**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="34ec6-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="34ec6-173">Hallo vNet maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-173">Create hello vNet.</span></span> <span data-ttu-id="34ec6-174">In dit voorbeeld sets Hallo virtueel netwerk naam toobe **myVnetName**, locatie te Hallo**VS-West**, en het adresvoorvoegsel voor het virtuele netwerk hello te Hallo**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="34ec6-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="34ec6-175">Netwerkbeveiligingsgroep hello en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="34ec6-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="34ec6-176">toobe kunnen toolog in tooyour VM met RDP, moet u een regel waarmee RDP-toegang op poort 3389 toohave.</span><span class="sxs-lookup"><span data-stu-id="34ec6-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="34ec6-177">Omdat hello VHD voor nieuwe virtuele machine is gemaakt vanuit een bestaande gespecialiseerde VM hello, kunt u een account van de virtuele bronmachine Hallo voor RDP.</span><span class="sxs-lookup"><span data-stu-id="34ec6-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="34ec6-178">In dit voorbeeld wordt de naam van het NSG te Hallo**myNsg** en Hallo RDP regelnaam te**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="34ec6-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="34ec6-179">Zie voor meer informatie over eindpunten en NSG-regels [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34ec6-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="34ec6-180">Een openbaar IP-adres en NIC maken</span><span class="sxs-lookup"><span data-stu-id="34ec6-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="34ec6-181">tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="34ec6-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="34ec6-182">Hallo openbare IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="34ec6-182">Create hello public IP.</span></span> <span data-ttu-id="34ec6-183">In dit voorbeeld Hallo naam openbare IP-adres te ingesteld**myIP**.</span><span class="sxs-lookup"><span data-stu-id="34ec6-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="34ec6-184">Hallo NIC. maken</span><span class="sxs-lookup"><span data-stu-id="34ec6-184">Create hello NIC.</span></span> <span data-ttu-id="34ec6-185">In dit voorbeeld Hallo NIC naam te is ingesteld**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="34ec6-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="34ec6-186">Hallo VM-naam en de grootte instellen</span><span class="sxs-lookup"><span data-stu-id="34ec6-186">Set hello VM name and size</span></span>

<span data-ttu-id="34ec6-187">In dit voorbeeld sets Hallo VM-naam te*myVM* en Hallo VM-grootte te*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="34ec6-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="34ec6-188">Hallo NIC toevoegen</span><span class="sxs-lookup"><span data-stu-id="34ec6-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="34ec6-189">Hallo OS-schijf toevoegen</span><span class="sxs-lookup"><span data-stu-id="34ec6-189">Add hello OS disk</span></span> 

<span data-ttu-id="34ec6-190">Toevoegen Hallo OS schijf toohello configuratie met behulp van [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="34ec6-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="34ec6-191">Dit voorbeeld wordt ingesteld Hallo grootte van Hallo schijf te*128 GB* en wordt Hallo-beheerde schijven als een *Windows* besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="34ec6-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="34ec6-192">Hallo VM voltooien</span><span class="sxs-lookup"><span data-stu-id="34ec6-192">Complete hello VM</span></span> 

<span data-ttu-id="34ec6-193">Maak Hallo-VM met [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)Hallo configuraties die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="34ec6-194">Als deze opdracht voltooid is, ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="34ec6-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="34ec6-195">Controleer of deze Hallo die VM is gemaakt</span><span class="sxs-lookup"><span data-stu-id="34ec6-195">Verify that hello VM was created</span></span>
<span data-ttu-id="34ec6-196">U ziet Hallo nieuw gemaakte VM in Hallo [Azure-portal](https://portal.azure.com)onder **Bladeren** > **virtuele machines**, of met behulp van de volgende PowerShell Hallo opdrachten:</span><span class="sxs-lookup"><span data-stu-id="34ec6-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="34ec6-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34ec6-197">Next steps</span></span>
<span data-ttu-id="34ec6-198">toosign in tooyour nieuwe virtuele machine, bladeren toohello VM in Hallo [portal](https://portal.azure.com), klikt u op **Connect**, en open Hallo Remote Desktop RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="34ec6-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="34ec6-199">Gebruik de accountreferenties op Hallo van uw oorspronkelijke toosign van de virtuele machine in tooyour nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="34ec6-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="34ec6-200">Zie voor meer informatie [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="34ec6-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

