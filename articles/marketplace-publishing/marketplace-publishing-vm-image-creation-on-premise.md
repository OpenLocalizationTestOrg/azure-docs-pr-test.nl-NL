---
title: een installatiekopie van een lokale virtuele machine voor hello Azure Marketplace aaaCreating | Microsoft Docs
description: Begrijpen en Hallo stappen toocreate een installatiekopie van een lokale virtuele machine uitvoeren en implementeren van toohello Azure Marketplace voor anderen toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="a8a73-103">Ontwikkelen van een installatiekopie van een lokale virtuele machine voor hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a8a73-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="a8a73-104">Het is raadzaam dat u Azure virtuele harde schijven (VHD's) rechtstreeks in de cloud Hallo ontwikkelen met behulp van Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="a8a73-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="a8a73-105">Als u moet het is echter mogelijk toodownload een VHD en het ontwikkelen met behulp van on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="a8a73-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="a8a73-106">Voor lokale ontwikkeling, moet u Hallo besturingssysteem VHD Hallo gemaakt downloaden VM.</span><span class="sxs-lookup"><span data-stu-id="a8a73-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="a8a73-107">Deze stappen zou worden uitgevoerd als onderdeel van de stap 3.3, hierboven.</span><span class="sxs-lookup"><span data-stu-id="a8a73-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="a8a73-108">Een VHD-installatiekopie te downloaden</span><span class="sxs-lookup"><span data-stu-id="a8a73-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="a8a73-109">Ga naar een blob-URL</span><span class="sxs-lookup"><span data-stu-id="a8a73-109">Locate a blob URL</span></span>
<span data-ttu-id="a8a73-110">In de volgorde toodownload Hallo VHD, moet u eerst Hallo blob-URL voor de besturingssysteemschijf Hallo vinden.</span><span class="sxs-lookup"><span data-stu-id="a8a73-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="a8a73-111">Zoek Hallo blob URL uit Hallo nieuwe [Microsoft Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="a8a73-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="a8a73-112">Ga te**Bladeren** > **VMs**, en selecteer vervolgens Hallo VM geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a8a73-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="a8a73-113">Onder **configureren**, selecteer Hallo **schijven** tegel, die Hallo schijven blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a8a73-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="a8a73-115">Selecteer Hallo **Besturingssysteemschijf**, waarmee u een andere blade die wordt weergegeven van de eigenschappen van de schijf, met inbegrip van de locatie van de VHD Hallo opent.</span><span class="sxs-lookup"><span data-stu-id="a8a73-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="a8a73-116">Kopieer deze blob-URL.</span><span class="sxs-lookup"><span data-stu-id="a8a73-116">Copy this blob URL.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="a8a73-118">Verwijder nu Hallo VM geïmplementeerd zonder Hallo back-ups maken schijven te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a8a73-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="a8a73-119">U kunt ook Hallo VM stoppen in plaats van te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a8a73-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="a8a73-120">Besturingssysteem-VHD Hallo niet downloaden wanneer Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a8a73-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="a8a73-122">Een VHD downloaden</span><span class="sxs-lookup"><span data-stu-id="a8a73-122">Download a VHD</span></span>
<span data-ttu-id="a8a73-123">Nadat u Hallo blob URL weet, kunt u Hallo VHD downloaden met behulp van Hallo [Azure-portal](http://manage.windowsazure.com/) of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8a73-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="a8a73-124">Gelijktijdig Hallo met het maken van deze handleiding is Hallo functionaliteit toodownload een VHD nog niet aanwezig in Hallo nieuwe Microsoft Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a8a73-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="a8a73-125">**Hallo besturingssysteem-VHD via Hallo huidige downloaden [Azure-portal](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="a8a73-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="a8a73-126">Meld u toohello Azure-portal als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="a8a73-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="a8a73-127">Klik op Hallo **opslag** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a8a73-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="a8a73-128">Selecteer Hallo storage-account in welke Hallo VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a8a73-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="a8a73-130">U ziet nu eigenschappen van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a8a73-130">This displays storage account properties.</span></span> <span data-ttu-id="a8a73-131">Selecteer Hallo **Containers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a8a73-131">Select hello **Containers** tab.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="a8a73-133">Selecteer Hallo-container in welke Hallo VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a8a73-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="a8a73-134">Standaard wanneer gemaakt vanuit de portal Hallo Hallo VHD opgeslagen in een VHD-container.</span><span class="sxs-lookup"><span data-stu-id="a8a73-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="a8a73-136">Selecteer Hallo juiste besturingssysteem-VHD door te vergelijken Hallo URL toohello een die u opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a8a73-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="a8a73-137">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="a8a73-137">Click **Download**.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="a8a73-139">Een VHD te downloaden met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8a73-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="a8a73-140">Bovendien toousing hello Azure-portal, kunt u Hallo [opslaan AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) besturingssysteem-cmdlet toodownload Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="a8a73-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="a8a73-141">Bijvoorbeeld opslaan-AzureVhd-bron "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath 'C:\Users\Administrator\Desktop\baseimagevm.vhd' - StorageKey<String></span><span class="sxs-lookup"><span data-stu-id="a8a73-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="a8a73-142">**Opslaan AzureVhd** heeft ook een **NumberOfThreads** optie die kan worden gebruikt tooincrease parallelle uitvoering toomake Hallo optimaal gebruik van de beschikbare bandbreedte voor Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="a8a73-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="a8a73-143">VHD's tooan Azure storage-account uploaden</span><span class="sxs-lookup"><span data-stu-id="a8a73-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="a8a73-144">Als u uw VHD's on-premises voorbereid, moet u deze in een opslag in Azure-account tooupload.</span><span class="sxs-lookup"><span data-stu-id="a8a73-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="a8a73-145">Deze stap vindt plaats nadat het maken van uw VHD lokale maar voordat het verkrijgen van de certificeringsinstantie voor uw VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a8a73-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="a8a73-146">Een opslagaccount en container maken</span><span class="sxs-lookup"><span data-stu-id="a8a73-146">Create a storage account and container</span></span>
<span data-ttu-id="a8a73-147">We raden aan dat de VHD's worden geüpload naar een opslagaccount in een regio in Hallo Verenigde Staten.</span><span class="sxs-lookup"><span data-stu-id="a8a73-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="a8a73-148">Alle VHD's voor een enkele SKU worden geplaatst in een enkele container binnen een enkele opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a8a73-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="a8a73-149">toocreate storage-account, kunt u Hallo [Microsoft Azure-portal](https://portal.azure.com/), PowerShell of Hallo Linux opdrachtregelhulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="a8a73-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="a8a73-150">**Een opslagaccount maken vanuit Hallo Microsoft Azure portal**</span><span class="sxs-lookup"><span data-stu-id="a8a73-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="a8a73-151">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a8a73-151">Click **New**.</span></span>
2. <span data-ttu-id="a8a73-152">Selecteer **opslag**.</span><span class="sxs-lookup"><span data-stu-id="a8a73-152">Select **Storage**.</span></span>
3. <span data-ttu-id="a8a73-153">Vul Hallo opslagaccountnaam en selecteer vervolgens een locatie.</span><span class="sxs-lookup"><span data-stu-id="a8a73-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="a8a73-155">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="a8a73-155">Click **Create**.</span></span>
5. <span data-ttu-id="a8a73-156">Hallo-blade voor Hallo storage-account gemaakt is geopend.</span><span class="sxs-lookup"><span data-stu-id="a8a73-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="a8a73-157">Zo niet, selecteer **Bladeren** > **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="a8a73-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="a8a73-158">Blade op Hallo Storage-account, selecteert u Hallo storage-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a8a73-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="a8a73-159">Selecteer **Containers**.</span><span class="sxs-lookup"><span data-stu-id="a8a73-159">Select **Containers**.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="a8a73-161">Selecteer op de blade Containers Hallo **toevoegen**, en voer een naam en het Hallo-container machtigingen voor de computercontainer.</span><span class="sxs-lookup"><span data-stu-id="a8a73-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="a8a73-162">Selecteer **persoonlijke** voor machtigingen van de container.</span><span class="sxs-lookup"><span data-stu-id="a8a73-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="a8a73-163">U wordt aangeraden dat u een container per SKU dat u van plan bent toopublish maken.</span><span class="sxs-lookup"><span data-stu-id="a8a73-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="a8a73-165">Een opslagaccount maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8a73-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="a8a73-166">Met behulp van PowerShell, een opslagaccount maken met behulp van Hallo [nieuw AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8a73-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="a8a73-167">Vervolgens u een container in dat storage-account maken kunt met behulp van Hallo [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8a73-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="a8a73-168">Deze opdrachten wordt ervan uitgegaan dat Hallo huidige storage account context is al ingesteld in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8a73-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="a8a73-169">Raadpleeg te[instellen van Azure PowerShell](marketplace-publishing-powershell-setup.md) voor meer informatie over de installatie van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8a73-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="a8a73-170">Een opslagaccount maken met behulp van Hallo-opdrachtregelprogramma voor Mac en Linux</span><span class="sxs-lookup"><span data-stu-id="a8a73-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="a8a73-171">Van [Linux opdrachtregelprogramma](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), als volgt een opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="a8a73-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="a8a73-172">Als volgt te werk om een container te maken.</span><span class="sxs-lookup"><span data-stu-id="a8a73-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="a8a73-173">Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="a8a73-173">Upload a VHD</span></span>
<span data-ttu-id="a8a73-174">Nadat het Hallo-opslagaccount en container worden gemaakt, kunt u uw voorbereide VHD's uploaden.</span><span class="sxs-lookup"><span data-stu-id="a8a73-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="a8a73-175">U kunt PowerShell, Hallo Linux opdrachtregelprogramma of andere Azure Storage management-hulpprogramma's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a8a73-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="a8a73-176">Een VHD via PowerShell uploaden</span><span class="sxs-lookup"><span data-stu-id="a8a73-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="a8a73-177">Gebruik Hallo [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a8a73-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="a8a73-178">Een VHD uploaden met Hallo-opdrachtregelprogramma voor Mac en Linux</span><span class="sxs-lookup"><span data-stu-id="a8a73-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="a8a73-179">Hello [Linux opdrachtregelprogramma](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), gebruikt u de volgende Hallo: azure vm-installatiekopie maken <image name> --locatie <Location of hello data center> --OS Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="a8a73-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="a8a73-180">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a8a73-180">See also</span></span>
* [<span data-ttu-id="a8a73-181">Maken van de installatiekopie van een virtuele machine voor Hallo Marketplace</span><span class="sxs-lookup"><span data-stu-id="a8a73-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="a8a73-182">Instellen van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8a73-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

