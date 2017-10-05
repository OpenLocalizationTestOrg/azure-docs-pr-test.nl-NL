---
title: Virtuele machine maken vanaf een speciale schijf in Azure | Microsoft Docs
description: Maak een nieuwe virtuele machine door het koppelen van een niet-beheerde gespecialiseerde schijf, in het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 974d89aa96cba94fedfd1acbaf4f1d30ac8e6257
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="79c1b-103">Een virtuele machine vanaf een speciale VHD in een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="79c1b-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="79c1b-104">Maak een nieuwe virtuele machine door het koppelen van een gespecialiseerde onbeheerde schijf als de OS-schijf met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="79c1b-104">Create a new VM by attaching a specialized unmanaged disk as the OS disk using Powershell.</span></span> <span data-ttu-id="79c1b-105">Een speciale schijf is een kopie van de VHD van een bestaande virtuele machine die de gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM onderhoudt.</span><span class="sxs-lookup"><span data-stu-id="79c1b-105">A specialized disk is a copy of VHD from an existing VM that maintains the user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="79c1b-106">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="79c1b-106">You have two options:</span></span>
* [<span data-ttu-id="79c1b-107">Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="79c1b-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="79c1b-108">Kopieer de VHD van een bestaande virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="79c1b-108">Copy the VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="79c1b-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="79c1b-109">Before you begin</span></span>
<span data-ttu-id="79c1b-110">Als u PowerShell gebruikt, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt.</span><span class="sxs-lookup"><span data-stu-id="79c1b-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="79c1b-111">Voer de volgende opdracht om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="79c1b-111">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="79c1b-112">Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79c1b-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="79c1b-113">Optie 1: Een gespecialiseerde VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="79c1b-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="79c1b-114">U kunt de VHD van een speciale virtuele machine gemaakt met een lokale virtualisatie hulpprogramma, zoals Hyper-V of een virtuele machine die zijn geëxporteerd uit een andere cloud uploaden.</span><span class="sxs-lookup"><span data-stu-id="79c1b-114">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="79c1b-115">De virtuele machine voorbereiden</span><span class="sxs-lookup"><span data-stu-id="79c1b-115">Prepare the VM</span></span>
<span data-ttu-id="79c1b-116">U kunt een gespecialiseerde VHD die is gemaakt met een lokale virtuele machine of een VHD die is geëxporteerd uit een andere cloud uploaden.</span><span class="sxs-lookup"><span data-stu-id="79c1b-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="79c1b-117">Een speciale VHD houdt de gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="79c1b-117">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="79c1b-118">Als u wilt gebruiken van de VHD-is een nieuwe virtuele machine maken, controleert u de volgende stappen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="79c1b-118">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="79c1b-119">[Voorbereiden van een Windows-VHD te uploaden naar Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79c1b-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="79c1b-120">**Geen** generalize van de virtuele machine met behulp van Sysprep.</span><span class="sxs-lookup"><span data-stu-id="79c1b-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="79c1b-121">Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op de virtuele machine (dat wil zeggen VMware tools).</span><span class="sxs-lookup"><span data-stu-id="79c1b-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="79c1b-122">Zorg ervoor dat de virtuele machine is geconfigureerd om op te halen van de IP-adres en DNS-instellingen via DHCP.</span><span class="sxs-lookup"><span data-stu-id="79c1b-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="79c1b-123">Dit zorgt ervoor dat de server een IP-adres binnen het VNet verkrijgt wanneer deze opgestart wordt.</span><span class="sxs-lookup"><span data-stu-id="79c1b-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="79c1b-124">Het storage-account ophalen</span><span class="sxs-lookup"><span data-stu-id="79c1b-124">Get the storage account</span></span>
<span data-ttu-id="79c1b-125">U moet een opslagaccount in Azure voor het opslaan van de installatiekopie van het geüploade VM.</span><span class="sxs-lookup"><span data-stu-id="79c1b-125">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="79c1b-126">U kunt een bestaand opslagaccount gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="79c1b-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="79c1b-127">Als u wilt de beschikbare opslagruimte accounts weergeven, typt u:</span><span class="sxs-lookup"><span data-stu-id="79c1b-127">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="79c1b-128">Als u een bestaand opslagaccount gebruiken wilt, gaat u verder met de [de VM-installatiekopie uploaden](#upload-the-vm-vhd-to-your-storage-account) sectie.</span><span class="sxs-lookup"><span data-stu-id="79c1b-128">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="79c1b-129">Als u wilt maken van een opslagaccount, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="79c1b-129">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="79c1b-130">U moet de naam van de resourcegroep waar het storage-account moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="79c1b-130">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="79c1b-131">Voor meer informatie over de resourcegroepen die zich in uw abonnement, typt u:</span><span class="sxs-lookup"><span data-stu-id="79c1b-131">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="79c1b-132">Maken van een resourcegroep met de naam **myResourceGroup** in de **VS-West** regio, type:</span><span class="sxs-lookup"><span data-stu-id="79c1b-132">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="79c1b-133">Maken van een opslagaccount met de naam **mystorageaccount** in deze resourcegroep met behulp van de [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="79c1b-133">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="79c1b-134">De VHD te uploaden naar uw opslagaccount</span><span class="sxs-lookup"><span data-stu-id="79c1b-134">Upload the VHD to your storage account</span></span>
<span data-ttu-id="79c1b-135">Gebruik de [toevoegen AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet voor het uploaden van de installatiekopie naar een container in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="79c1b-135">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="79c1b-136">In dit voorbeeld wordt het bestand geüpload **myVHD.vhd** van `"C:\Users\Public\Documents\Virtual hard disks\"` om een opslagaccount met de naam **mystorageaccount** in de **myResourceGroup** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="79c1b-136">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="79c1b-137">Het bestand worden opgenomen in de container met de naam **mycontainer** en worden de nieuwe bestandsnaam **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-137">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="79c1b-138">Als dit lukt, kunt u krijgen een antwoord dat ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="79c1b-138">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="79c1b-139">Afhankelijk van uw netwerkverbinding en de grootte van de VHD-bestand kan met deze opdracht duren om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="79c1b-139">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="option-2-copy-the-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="79c1b-140">Optie 2: Kopieer de VHD van een bestaande virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="79c1b-140">Option 2: Copy the VHD from an existing Azure VM</span></span>

<span data-ttu-id="79c1b-141">U kunt een VHD kopiëren naar een ander opslagaccount te gebruiken bij het maken van een nieuwe, dubbele virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79c1b-141">You can copy a VHD to another storage account to use when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="79c1b-142">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="79c1b-142">Before you begin</span></span>
<span data-ttu-id="79c1b-143">Zorg ervoor dat u:</span><span class="sxs-lookup"><span data-stu-id="79c1b-143">Make sure that you:</span></span>

* <span data-ttu-id="79c1b-144">Hebt u informatie over de **bron- en storage-accounts**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-144">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="79c1b-145">Voor de bron-VM moet u de namen van de storage-account en container hebt.</span><span class="sxs-lookup"><span data-stu-id="79c1b-145">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="79c1b-146">Normaal gesproken de containernaam is **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-146">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="79c1b-147">U moet ook een doelopslagaccount hebben.</span><span class="sxs-lookup"><span data-stu-id="79c1b-147">You also need to have a destination storage account.</span></span> <span data-ttu-id="79c1b-148">Als u dit niet al hebt, kunt u een met ofwel de portal (**meer Services** > opslagaccounts > toevoegen) of met behulp van de [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="79c1b-148">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="79c1b-149">Hebt gedownload en geïnstalleerd de [AzCopy hulpprogramma](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="79c1b-149">Have downloaded and installed the [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-the-vm"></a><span data-ttu-id="79c1b-150">De virtuele machine ongedaan</span><span class="sxs-lookup"><span data-stu-id="79c1b-150">Deallocate the VM</span></span>
<span data-ttu-id="79c1b-151">Toewijzing van de VM, u de VHD maakt moet worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="79c1b-151">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="79c1b-152">**Portal**: klik op **virtuele machines** > **myVM** > stoppen</span><span class="sxs-lookup"><span data-stu-id="79c1b-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="79c1b-153">**PowerShell**: Gebruik [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) gestopt (toewijzing ongedaan maken) de virtuele machine met de naam **myVM** in de resourcegroep **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) to stop (deallocate) the VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="79c1b-154">De **Status** voor de virtuele machine in Azure portal wordt gewijzigd van **gestopt** naar **gestopt (toewijzing opgeheven)**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-154">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

### <a name="get-the-storage-account-urls"></a><span data-ttu-id="79c1b-155">De storage-account-URL's ophalen</span><span class="sxs-lookup"><span data-stu-id="79c1b-155">Get the storage account URLs</span></span>
<span data-ttu-id="79c1b-156">U moet de URL's van de bron- en storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="79c1b-156">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="79c1b-157">De URL's eruit: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="79c1b-157">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="79c1b-158">Als u de naam van de storage-account en de container al weet, kunt u alleen de gegevens tussen de vierkante haken voor het maken van de URL van uw vervangen.</span><span class="sxs-lookup"><span data-stu-id="79c1b-158">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="79c1b-159">U kunt de Azure portal of Azure Powershell gebruiken om de URL te krijgen:</span><span class="sxs-lookup"><span data-stu-id="79c1b-159">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="79c1b-160">**Portal**: klik op de  **>**  voor **meer services** > **opslagaccounts**  >   *Storage-account* > **Blobs** en de bron-VHD-bestand is waarschijnlijk in de **VHD's** container.</span><span class="sxs-lookup"><span data-stu-id="79c1b-160">**Portal**: Click the **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="79c1b-161">Klik op **eigenschappen** voor de container en kopieer de tekst met het label **URL**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-161">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="79c1b-162">U moet de URL's van de bron- en doelserver containers.</span><span class="sxs-lookup"><span data-stu-id="79c1b-162">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="79c1b-163">**PowerShell**: Gebruik [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) ophalen van de gegevens voor de virtuele machine met de naam **myVM** in de resourcegroep **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) to get the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="79c1b-164">Zoeken in de resultaten in de **archiefprofiel** sectie voor de **Vhd-Uri**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-164">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="79c1b-165">Het eerste deel van de Uri is de URL van de container en het laatste deel is de naam van de OS-VHD voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79c1b-165">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="79c1b-166">Ophalen van de toegangssleutels voor opslag</span><span class="sxs-lookup"><span data-stu-id="79c1b-166">Get the storage access keys</span></span>
<span data-ttu-id="79c1b-167">De sneltoetsen voor de bron- en storage-accounts vinden.</span><span class="sxs-lookup"><span data-stu-id="79c1b-167">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="79c1b-168">Zie voor meer informatie over toegangstoetsen [over Azure storage-accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="79c1b-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="79c1b-169">**Portal**: klik op **meer services** > **opslagaccounts** > *opslagaccount*  >  **Toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="79c1b-170">Kopieer de sleutel met het label **key1**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-170">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="79c1b-171">**PowerShell**: Gebruik [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) ophalen van de opslagsleutel voor het opslagaccount **mystorageaccount** in de resourcegroep **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) to get the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="79c1b-172">Kopieer de sleutel met het label **key1**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-172">Copy the key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-the-vhd"></a><span data-ttu-id="79c1b-173">Kopieer de VHD</span><span class="sxs-lookup"><span data-stu-id="79c1b-173">Copy the VHD</span></span>
<span data-ttu-id="79c1b-174">U kunt bestanden kopiëren tussen opslagaccounts met behulp van AzCopy.</span><span class="sxs-lookup"><span data-stu-id="79c1b-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="79c1b-175">Voor de doelcontainer als de opgegeven container niet bestaat, wordt deze gemaakt voor u.</span><span class="sxs-lookup"><span data-stu-id="79c1b-175">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="79c1b-176">Open een opdrachtprompt op uw lokale computer voor het gebruik van AzCopy en navigeer naar de map waarin AzCopy is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="79c1b-176">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="79c1b-177">Dit is vergelijkbaar met *C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="79c1b-177">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="79c1b-178">Alle bestanden in een container wilt kopiëren, gebruikt u de **/S** overschakelen.</span><span class="sxs-lookup"><span data-stu-id="79c1b-178">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="79c1b-179">Dit kan worden gebruikt voor het kopiëren van de OS-VHD en alle gegevensschijven van de als deze zich in dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="79c1b-179">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="79c1b-180">Dit voorbeeld ziet u hoe u kopieert u alle bestanden in de container **mysourcecontainer** in opslagaccount **mysourcestorageaccount** aan de container **mydestinationcontainer**in de **mydestinationstorageaccount** storage-account.</span><span class="sxs-lookup"><span data-stu-id="79c1b-180">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="79c1b-181">De namen van de storage-accounts en containers vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="79c1b-181">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="79c1b-182">Vervang `<sourceStorageAccountKey1>` en `<destinationStorageAccountKey1>` met uw eigen sleutels.</span><span class="sxs-lookup"><span data-stu-id="79c1b-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="79c1b-183">Als u wilt kopiëren van een specifieke VHD in een container met meerdere bestanden, kunt u ook de naam van het bestand met de schakeloptie /Pattern opgeven.</span><span class="sxs-lookup"><span data-stu-id="79c1b-183">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="79c1b-184">In dit voorbeeld wordt alleen het bestand met de naam **myFileName.vhd** worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="79c1b-184">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="79c1b-185">Als dit is voltooid, ontvangt u een bericht dat ongeveer als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="79c1b-185">When it is finished, you will get a message that looks something like:</span></span>

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

### <a name="troubleshooting"></a><span data-ttu-id="79c1b-186">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="79c1b-186">Troubleshooting</span></span>
* <span data-ttu-id="79c1b-187">Wanneer u met AZCopy, als de foutmelding 'Kan niet verifiëren van de aanvraag Server', zorg ervoor dat de waarde van de autorisatie-header is een samengesteld correct met inbegrip van de handtekening.</span><span class="sxs-lookup"><span data-stu-id="79c1b-187">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="79c1b-188">Als u sleutel 2 of de sleutel van de secundaire opslag gebruikt, probeert u de primaire of 1e-opslagsleutel.</span><span class="sxs-lookup"><span data-stu-id="79c1b-188">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="create-the-new-vm"></a><span data-ttu-id="79c1b-189">De nieuwe virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="79c1b-189">Create the new VM</span></span> 

<span data-ttu-id="79c1b-190">U moet maken van netwerken en andere VM-netwerkbronnen kunnen worden gebruikt door de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79c1b-190">You need to create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="79c1b-191">Het subNet en een vNet maken</span><span class="sxs-lookup"><span data-stu-id="79c1b-191">Create the subNet and vNet</span></span>

<span data-ttu-id="79c1b-192">Maken van het vNet en het subNet van de [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79c1b-192">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="79c1b-193">Het subNet maken.</span><span class="sxs-lookup"><span data-stu-id="79c1b-193">Create the subNet.</span></span> <span data-ttu-id="79c1b-194">In dit voorbeeld wordt een subnet met de naam **mySubNet**, in de resourcegroep **myResourceGroup**, en stelt u het adres subnetvoorvoegsel op **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-194">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="79c1b-195">Het vNet maken.</span><span class="sxs-lookup"><span data-stu-id="79c1b-195">Create the vNet.</span></span> <span data-ttu-id="79c1b-196">Dit voorbeeld wordt de naam van het virtuele netwerk moet **myVnetName**, de locatie voor het **VS-West**, en het adresvoorvoegsel voor het virtuele netwerk naar **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-196">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="79c1b-197">Een openbaar IP-adres en NIC maken</span><span class="sxs-lookup"><span data-stu-id="79c1b-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="79c1b-198">Om te kunnen communiceren met de virtuele machine in het virtuele netwerk, hebt u een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) en een netwerkinterface nodig.</span><span class="sxs-lookup"><span data-stu-id="79c1b-198">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="79c1b-199">Het openbare IP-adres maken.</span><span class="sxs-lookup"><span data-stu-id="79c1b-199">Create the public IP.</span></span> <span data-ttu-id="79c1b-200">In dit voorbeeld wordt de openbare naam van de IP-adres is ingesteld op **myIP**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-200">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="79c1b-201">Maken van de NIC.</span><span class="sxs-lookup"><span data-stu-id="79c1b-201">Create the NIC.</span></span> <span data-ttu-id="79c1b-202">In dit voorbeeld wordt de naam van de NIC is ingesteld op **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-202">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="79c1b-203">De netwerkbeveiligingsgroep en een RDP-regel maken</span><span class="sxs-lookup"><span data-stu-id="79c1b-203">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="79c1b-204">Als u zich aanmelden bij uw virtuele machine met RDP, moet u een regel waarmee op poort 3389 van RDP-toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="79c1b-204">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="79c1b-205">Omdat de VHD voor de nieuwe virtuele machine is gemaakt van een bestaand kunt gespecialiseerde VM, nadat de virtuele machine u maakt een bestaand account van de virtuele bronmachine die machtiging aan te melden met RDP had gebruiken.</span><span class="sxs-lookup"><span data-stu-id="79c1b-205">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="79c1b-206">In het volgende voorbeeld wordt de naam van de NSG op **myNsg** en de naam van de RDP-regel aan **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-206">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="79c1b-207">Zie voor meer informatie over eindpunten en NSG-regels [openen van poorten voor een virtuele machine in Azure met behulp van PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79c1b-207">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="79c1b-208">VM-naam en de grootte instellen</span><span class="sxs-lookup"><span data-stu-id="79c1b-208">Set the VM name and size</span></span>

<span data-ttu-id="79c1b-209">Dit voorbeeld wordt de naam van de VM naar 'myVM' en de VM-grootte naar 'Standard_A2'.</span><span class="sxs-lookup"><span data-stu-id="79c1b-209">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="79c1b-210">De NIC toevoegen</span><span class="sxs-lookup"><span data-stu-id="79c1b-210">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-the-os-disk"></a><span data-ttu-id="79c1b-211">Configureer de OS-schijf</span><span class="sxs-lookup"><span data-stu-id="79c1b-211">Configure the OS disk</span></span>

1. <span data-ttu-id="79c1b-212">Stel de URI voor de VHD die u hebt geüpload of gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="79c1b-212">Set the URI for the VHD that you uploaded or copied.</span></span> <span data-ttu-id="79c1b-213">In dit voorbeeld wordt het VHD-bestand met de naam **myOsDisk.vhd** wordt opgeslagen in een opslagaccount met de naam **myStorageAccount** in een container met de naam **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="79c1b-213">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="79c1b-214">De OS-schijf toevoegen.</span><span class="sxs-lookup"><span data-stu-id="79c1b-214">Add the OS disk.</span></span> <span data-ttu-id="79c1b-215">Wanneer de besturingssysteemschijf is gemaakt, is de term 'osDisk' in dit voorbeeld appened op de VM-naam voor het maken van de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="79c1b-215">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="79c1b-216">In dit voorbeeld geeft ook dat deze VHD op basis van Windows moet worden gekoppeld aan de virtuele machine als de besturingssysteemschijf.</span><span class="sxs-lookup"><span data-stu-id="79c1b-216">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="79c1b-217">Optioneel: Als u gegevensschijven die moeten worden gekoppeld aan de virtuele machine hebt, de gegevensschijven toevoegen met behulp van de URL's van de gegevens van virtuele harde schijven en de juiste Logical Unit Number (Lun).</span><span class="sxs-lookup"><span data-stu-id="79c1b-217">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="79c1b-218">Wanneer u een opslagaccount, de gegevens en de URL's van besturingssysteem schijf als volgt uitzien: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="79c1b-218">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="79c1b-219">U kunt dit vinden op de portal bladeren naar de doel-storage-container, klikt u op het besturingssysteem of gegevens VHD die is gekopieerd en vervolgens de inhoud van de URL te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="79c1b-219">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


### <a name="complete-the-vm"></a><span data-ttu-id="79c1b-220">De virtuele machine voltooien</span><span class="sxs-lookup"><span data-stu-id="79c1b-220">Complete the VM</span></span> 

<span data-ttu-id="79c1b-221">De virtuele machine maken met de configuraties die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="79c1b-221">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="79c1b-222">Als deze opdracht voltooid is, ziet u uitvoer als volgt:</span><span class="sxs-lookup"><span data-stu-id="79c1b-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="79c1b-223">Controleren of de virtuele machine is gemaakt</span><span class="sxs-lookup"><span data-stu-id="79c1b-223">Verify that the VM was created</span></span>
<span data-ttu-id="79c1b-224">U ziet de zojuist gemaakte virtuele machine ofwel in de [Azure-portal](https://portal.azure.com)onder **Bladeren** > **virtuele machines**, of met behulp van de volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="79c1b-224">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="79c1b-225">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79c1b-225">Next steps</span></span>
<span data-ttu-id="79c1b-226">Als u wilt aanmelden bij uw nieuwe virtuele machine, blader naar de virtuele machine in de [portal](https://portal.azure.com), klikt u op **Connect**, en open het RDP-Remote Desktop-bestand.</span><span class="sxs-lookup"><span data-stu-id="79c1b-226">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="79c1b-227">Gebruik de referenties van het account van uw oorspronkelijke virtuele machine aan te melden bij uw nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79c1b-227">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="79c1b-228">Zie voor meer informatie [verbinding maken met en meld u aan een virtuele machine van Azure waarop Windows wordt uitgevoerd bij](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="79c1b-228">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

