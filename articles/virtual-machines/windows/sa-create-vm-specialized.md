---
title: aaaCreate VM vanaf een speciale schijf in Azure | Microsoft Docs
description: Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde onbeheerde schijf Hallo Resource Manager-implementatiemodel.
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="7f950-103">Een virtuele machine vanaf een speciale VHD in een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="7f950-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="7f950-104">Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde onbeheerde schijf als Hallo besturingssysteemschijf met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="7f950-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="7f950-105">Een speciale schijf is een kopie van de VHD van een bestaande virtuele machine die wordt onderhouden door Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="7f950-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="7f950-106">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="7f950-106">You have two options:</span></span>
* [<span data-ttu-id="7f950-107">Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="7f950-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="7f950-108">Kopieer Hallo VHD van een bestaande virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="7f950-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="7f950-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7f950-109">Before you begin</span></span>
<span data-ttu-id="7f950-110">Als u PowerShell gebruikt, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="7f950-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="7f950-111">Voer Hallo na de opdracht tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="7f950-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="7f950-112">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7f950-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="7f950-113">Optie 1: Een gespecialiseerde VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="7f950-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="7f950-114">U kunt VHD van een speciale virtuele machine met een lokale virtualisatie hulpprogramma gemaakt, zoals Hyper-V of een virtuele machine die zijn geëxporteerd uit een andere cloud Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="7f950-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="7f950-115">Hallo VM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7f950-115">Prepare hello VM</span></span>
<span data-ttu-id="7f950-116">U kunt een gespecialiseerde VHD die is gemaakt met een lokale virtuele machine of een VHD die is geëxporteerd uit een andere cloud uploaden.</span><span class="sxs-lookup"><span data-stu-id="7f950-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="7f950-117">Een speciale VHD onderhoudt Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="7f950-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="7f950-118">Als u van plan toouse bent Hallo VHD-toocreate is een nieuwe virtuele machine, Controleer Hallo stappen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="7f950-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="7f950-119">[Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f950-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7f950-120">**Geen** generalize Hallo van virtuele machine met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="7f950-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="7f950-121">Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op Hallo VM (dat wil zeggen VMware tools).</span><span class="sxs-lookup"><span data-stu-id="7f950-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="7f950-122">Zorg ervoor dat Hallo VM geconfigureerde toopull is het IP-adres en DNS-instellingen via DHCP.</span><span class="sxs-lookup"><span data-stu-id="7f950-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="7f950-123">Dit zorgt ervoor dat Hallo-server verkrijgt IP-adres binnen Hallo VNet wanneer deze opgestart wordt.</span><span class="sxs-lookup"><span data-stu-id="7f950-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="7f950-124">Hallo storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="7f950-124">Get hello storage account</span></span>
<span data-ttu-id="7f950-125">U moet een opslagaccount in Azure toostore Hallo geüpload VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7f950-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="7f950-126">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="7f950-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="7f950-127">tooshow hello beschikbaar storage-accounts, typt u:</span><span class="sxs-lookup"><span data-stu-id="7f950-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="7f950-128">Als u een bestaand opslagaccount toouse wilt, gaat u verder toohello [Hallo VM-installatiekopie uploaden](#upload-the-vm-vhd-to-your-storage-account) sectie.</span><span class="sxs-lookup"><span data-stu-id="7f950-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="7f950-129">Als u een opslagaccount toocreate moet, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="7f950-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="7f950-130">U moet Hallo-naam van resourcegroep Hallo waar Hallo storage-account moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f950-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="7f950-131">toofind uit alle Hallo resourcegroepen in uw abonnement, type:</span><span class="sxs-lookup"><span data-stu-id="7f950-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="7f950-132">een resourcegroep met de naam toocreate **myResourceGroup** in Hallo **VS-West** regio, type:</span><span class="sxs-lookup"><span data-stu-id="7f950-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="7f950-133">Maken van een opslagaccount met de naam **mystorageaccount** in deze resourcegroep via Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7f950-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="7f950-134">Hallo VHD tooyour storage-account uploaden</span><span class="sxs-lookup"><span data-stu-id="7f950-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="7f950-135">Gebruik Hallo [toevoegen AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload Hallo installatiekopie tooa container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7f950-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="7f950-136">In dit voorbeeld uploads Hallo bestand **myVHD.vhd** van `"C:\Users\Public\Documents\Virtual hard disks\"` tooa opslagaccount met de naam **mystorageaccount** in Hallo **myResourceGroup** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7f950-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="7f950-137">Hallo-bestand worden opgenomen in het Hallo-container met de naam **mycontainer** en worden nieuwe bestandsnaam Hallo **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="7f950-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="7f950-138">Als dit lukt, kunt u een antwoord dat vergelijkbare toothis lijkt krijgen:</span><span class="sxs-lookup"><span data-stu-id="7f950-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="7f950-139">Afhankelijk van uw netwerkverbinding en het Hallo-grootte van het VHD-bestand met deze opdracht kan een tijdje duren toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7f950-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="7f950-140">Optie 2: Kopieer Hallo VHD van een bestaande virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="7f950-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="7f950-141">Bij het maken van een nieuwe, dubbele virtuele machine, kunt u een VHD tooanother storage account toouse kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7f950-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="7f950-142">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7f950-142">Before you begin</span></span>
<span data-ttu-id="7f950-143">Zorg ervoor dat u:</span><span class="sxs-lookup"><span data-stu-id="7f950-143">Make sure that you:</span></span>

* <span data-ttu-id="7f950-144">Informatie over Hallo **bron- en storage-accounts**.</span><span class="sxs-lookup"><span data-stu-id="7f950-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="7f950-145">Hallo bron-VM moet u toohave Hallo storage-account en de container namen.</span><span class="sxs-lookup"><span data-stu-id="7f950-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="7f950-146">Normaal gesproken Hallo containernaam worden **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="7f950-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="7f950-147">U moet ook een doelopslagaccount toohave.</span><span class="sxs-lookup"><span data-stu-id="7f950-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="7f950-148">Als u dit niet al hebt, kunt u een met een van de portals hello (**meer Services** > opslagaccounts > toevoegen) of met behulp van Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7f950-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="7f950-149">Hebt gedownload en geïnstalleerd Hallo [AzCopy hulpprogramma](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="7f950-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="7f950-150">Hallo VM ongedaan gemaakt</span><span class="sxs-lookup"><span data-stu-id="7f950-150">Deallocate hello VM</span></span>
<span data-ttu-id="7f950-151">Toewijzing Hallo virtuele machine vrijgemaakt Hallo VHD toobe gekopieerd wordt.</span><span class="sxs-lookup"><span data-stu-id="7f950-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="7f950-152">**Portal**: klik op **virtuele machines** > **myVM** > stoppen</span><span class="sxs-lookup"><span data-stu-id="7f950-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="7f950-153">**PowerShell**: Gebruik [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (ongedaan gemaakt) met de naam VM Hallo **myVM** in de resourcegroep **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7f950-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="7f950-154">Hallo **Status** voor Hallo VM in hello Azure portal wordt gewijzigd van **gestopt** te**gestopt (toewijzing opgeheven)**.</span><span class="sxs-lookup"><span data-stu-id="7f950-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="7f950-155">Hallo storage-account-URL's ophalen</span><span class="sxs-lookup"><span data-stu-id="7f950-155">Get hello storage account URLs</span></span>
<span data-ttu-id="7f950-156">U moet Hallo-URL's van Hallo bron- en storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="7f950-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="7f950-157">Hallo URL er als volgt uitzien: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="7f950-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="7f950-158">Als u al Hallo-account en de container Opslagnaam weet, kunt u zojuist hebt vervangen Hallo informatie tussen Hallo haken toocreate uw URL.</span><span class="sxs-lookup"><span data-stu-id="7f950-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="7f950-159">U kunt hello Azure-portal of Azure Powershell tooget Hallo URL gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7f950-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="7f950-160">**Portal**: klik op Hallo  **>**  voor **meer services** > **opslagaccounts**  >   *Storage-account* > **Blobs** en de bron-VHD-bestand is waarschijnlijk in Hallo **VHD's** container.</span><span class="sxs-lookup"><span data-stu-id="7f950-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="7f950-161">Klik op **eigenschappen** voor Hallo-container en de tekst hello kopiëren met het label **URL**.</span><span class="sxs-lookup"><span data-stu-id="7f950-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="7f950-162">U moet Hallo-URL's van beide Hallo bron- en doelserver containers.</span><span class="sxs-lookup"><span data-stu-id="7f950-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="7f950-163">**PowerShell**: Gebruik [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget Hallo-informatie voor de virtuele machine met de naam **myVM** in de resourcegroep Hallo **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7f950-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="7f950-164">Hallo-resultaten, kijk in Hallo **archiefprofiel** sectie voor Hallo **Vhd-Uri**.</span><span class="sxs-lookup"><span data-stu-id="7f950-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="7f950-165">Hallo eerste deel van Hallo Uri is Hallo URL toohello container en het laatste deel Hallo is Hallo OS VHD-naam voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="7f950-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="7f950-166">Hallo opslagtoegangssleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="7f950-166">Get hello storage access keys</span></span>
<span data-ttu-id="7f950-167">Hallo toegangstoetsen voor Hallo bron- en storage-accounts gevonden.</span><span class="sxs-lookup"><span data-stu-id="7f950-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="7f950-168">Zie voor meer informatie over toegangstoetsen [over Azure storage-accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7f950-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="7f950-169">**Portal**: klik op **meer services** > **opslagaccounts** > *opslagaccount*  >  **Toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="7f950-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="7f950-170">Kopiëren Hallo sleutel aangeduid als **key1**.</span><span class="sxs-lookup"><span data-stu-id="7f950-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="7f950-171">**PowerShell**: Gebruik [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget Hallo-opslagsleutel voor opslagaccount hello **mystorageaccount** in de resourcegroep Hallo  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="7f950-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="7f950-172">Kopiëren Hallo sleutel met het label **key1**.</span><span class="sxs-lookup"><span data-stu-id="7f950-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="7f950-173">Hallo VHD kopiëren</span><span class="sxs-lookup"><span data-stu-id="7f950-173">Copy hello VHD</span></span>
<span data-ttu-id="7f950-174">U kunt bestanden kopiëren tussen opslagaccounts met behulp van AzCopy.</span><span class="sxs-lookup"><span data-stu-id="7f950-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="7f950-175">Voor de doelcontainer hello, als de opgegeven container Hallo niet bestaat, zal deze worden voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f950-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="7f950-176">toouse AzCopy, open een opdrachtprompt op uw lokale machine en navigeer toohello-map waarin AzCopy is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7f950-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="7f950-177">Deze lijken te*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="7f950-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="7f950-178">toocopy alle Hallo bestanden binnen een container, gebruikt u Hallo **/S** overschakelen.</span><span class="sxs-lookup"><span data-stu-id="7f950-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="7f950-179">Dit kan gebruikte toocopy Hallo OS VHD en alle Hallo gegevensschijven als ze in dezelfde container Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f950-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="7f950-180">Dit voorbeeld ziet u hoe alle Hallo bestanden in de container Hallo toocopy **mysourcecontainer** in opslagaccount **mysourcestorageaccount** toohello container **mydestinationcontainer**  in Hallo **mydestinationstorageaccount** storage-account.</span><span class="sxs-lookup"><span data-stu-id="7f950-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="7f950-181">Hallo-namen van opslagaccounts hello en containers vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="7f950-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="7f950-182">Vervang `<sourceStorageAccountKey1>` en `<destinationStorageAccountKey1>` met uw eigen sleutels.</span><span class="sxs-lookup"><span data-stu-id="7f950-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="7f950-183">Als u wilt dat alleen toocopy een specifieke VHD in een container met meerdere bestanden, kunt u ook Hallo bestandsnaam met Hallo /Pattern switch opgeven.</span><span class="sxs-lookup"><span data-stu-id="7f950-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="7f950-184">In dit voorbeeld bestand met de naam alleen Hallo **myFileName.vhd** worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7f950-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="7f950-185">Als dit is voltooid, ontvangt u een bericht dat ongeveer als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="7f950-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="7f950-186">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7f950-186">Troubleshooting</span></span>
* <span data-ttu-id="7f950-187">Wanneer u met AZCopy, als er een fout Hallo 'Server is mislukt tooauthenticate Hallo aanvraag', zorg er dan voor dat Hallo-waarde van de autorisatie-header Hallo correct inclusief Hallo handtekening is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="7f950-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="7f950-188">Als u sleutel 2 of Hallo secundaire opslagsleutel gebruikt, probeert u de primaire of 1e opslagsleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f950-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="7f950-189">Maken van nieuwe virtuele machine Hallo</span><span class="sxs-lookup"><span data-stu-id="7f950-189">Create hello new VM</span></span> 

<span data-ttu-id="7f950-190">U moet toocreate netwerken en andere VM-resources toobe die wordt gebruikt door Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7f950-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="7f950-191">Hallo-subNet en een vNet maken</span><span class="sxs-lookup"><span data-stu-id="7f950-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="7f950-192">Hallo vNet en subNet Hallo maken [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f950-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="7f950-193">Hallo subNet maken.</span><span class="sxs-lookup"><span data-stu-id="7f950-193">Create hello subNet.</span></span> <span data-ttu-id="7f950-194">In dit voorbeeld wordt een subnet met de naam **mySubNet**, in de resourcegroep Hallo **myResourceGroup**, en stelt Hallo adresvoorvoegsel subnet te**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="7f950-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="7f950-195">Hallo vNet maken.</span><span class="sxs-lookup"><span data-stu-id="7f950-195">Create hello vNet.</span></span> <span data-ttu-id="7f950-196">In dit voorbeeld sets Hallo virtueel netwerk naam toobe **myVnetName**, locatie te Hallo**VS-West**, en het adresvoorvoegsel voor het virtuele netwerk hello te Hallo**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="7f950-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="7f950-197">Een openbaar IP-adres en NIC maken</span><span class="sxs-lookup"><span data-stu-id="7f950-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="7f950-198">tooenable communicatie met Hallo virtuele machine in het virtuele netwerk hello, moet u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="7f950-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="7f950-199">Hallo openbare IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="7f950-199">Create hello public IP.</span></span> <span data-ttu-id="7f950-200">In dit voorbeeld Hallo naam openbare IP-adres te ingesteld**myIP**.</span><span class="sxs-lookup"><span data-stu-id="7f950-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="7f950-201">Hallo NIC. maken</span><span class="sxs-lookup"><span data-stu-id="7f950-201">Create hello NIC.</span></span> <span data-ttu-id="7f950-202">In dit voorbeeld Hallo NIC naam te is ingesteld**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="7f950-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="7f950-203">Netwerkbeveiligingsgroep hello en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="7f950-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="7f950-204">toobe kunnen toolog in tooyour VM met RDP, moet u toohave een beveiligingsregel waarmee op poort 3389 van RDP-toegang.</span><span class="sxs-lookup"><span data-stu-id="7f950-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="7f950-205">Omdat Hallo VHD voor de nieuwe virtuele machine is gemaakt van een bestaand Hallo gespecialiseerde kunt VM, nadat Hallo VM is gemaakt, moet u een bestaand account van Hallo virtuele bronmachine die machtiging toolog over het gebruik van RDP had gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7f950-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="7f950-206">In dit voorbeeld wordt de naam van het NSG te Hallo**myNsg** en Hallo RDP regelnaam te**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="7f950-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="7f950-207">Zie voor meer informatie over eindpunten en NSG-regels [openen van poorten tooa VM in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f950-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="7f950-208">Hallo VM-naam en de grootte instellen</span><span class="sxs-lookup"><span data-stu-id="7f950-208">Set hello VM name and size</span></span>

<span data-ttu-id="7f950-209">In dit voorbeeld sets Hallo VM-naam te 'myVM' en Hallo VM grootte te 'Standard_A2'.</span><span class="sxs-lookup"><span data-stu-id="7f950-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="7f950-210">Hallo NIC toevoegen</span><span class="sxs-lookup"><span data-stu-id="7f950-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="7f950-211">Configureer Hallo OS-schijf</span><span class="sxs-lookup"><span data-stu-id="7f950-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="7f950-212">Stel Hallo URI voor Hallo VHD die u hebt geüpload of gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7f950-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="7f950-213">In dit voorbeeld Hallo VHD-bestand met de naam **myOsDisk.vhd** wordt opgeslagen in een opslagaccount met de naam **myStorageAccount** in een container met de naam **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="7f950-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="7f950-214">Hallo OS-schijf toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7f950-214">Add hello OS disk.</span></span> <span data-ttu-id="7f950-215">Wanneer Hallo besturingssysteemschijf is gemaakt, is osDisk' hello term' in dit voorbeeld appened toohello VM naam toocreate Hallo naam Besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="7f950-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="7f950-216">In dit voorbeeld geeft ook dat deze VHD op basis van Windows gekoppelde toohello VM als Hallo OS-schijf moet worden.</span><span class="sxs-lookup"><span data-stu-id="7f950-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="7f950-217">Optioneel: Als u gegevensschijven hebt die moeten toobe gekoppeld toohello VM en voeg Hallo gegevensschijven met behulp van URL's van gegevens VHD's Hallo Hallo juiste Logical Unit Number (Lun).</span><span class="sxs-lookup"><span data-stu-id="7f950-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="7f950-218">Wanneer u een opslagaccount, Hallo gegevens en URL's van besturingssysteem schijf als volgt uitzien: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="7f950-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="7f950-219">U kunt dit vinden op Hallo portal door bladeren toohello doel storage-container, klikt u op Hallo besturingssysteem of gegevens VHD die is gekopieerd en vervolgens inhoud Hallo van Hallo-URL te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7f950-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="7f950-220">Hallo VM voltooien</span><span class="sxs-lookup"><span data-stu-id="7f950-220">Complete hello VM</span></span> 

<span data-ttu-id="7f950-221">Maak Hallo VM die gebruikmaakt van Hallo-configuraties die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7f950-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="7f950-222">Als deze opdracht voltooid is, ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="7f950-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="7f950-223">Controleer of deze Hallo die VM is gemaakt</span><span class="sxs-lookup"><span data-stu-id="7f950-223">Verify that hello VM was created</span></span>
<span data-ttu-id="7f950-224">U ziet Hallo nieuw gemaakte VM in Hallo [Azure-portal](https://portal.azure.com)onder **Bladeren** > **virtuele machines**, of met behulp van de volgende PowerShell Hallo opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7f950-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="7f950-225">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f950-225">Next steps</span></span>
<span data-ttu-id="7f950-226">toosign in tooyour nieuwe virtuele machine, bladeren toohello VM in Hallo [portal](https://portal.azure.com), klikt u op **Connect**, en open Hallo Remote Desktop RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="7f950-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="7f950-227">Gebruik de accountreferenties op Hallo van uw oorspronkelijke toosign van de virtuele machine in tooyour nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7f950-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="7f950-228">Zie voor meer informatie [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="7f950-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

