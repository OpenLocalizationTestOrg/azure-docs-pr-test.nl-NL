---
title: Maken van een installatiekopie van een lokale virtuele machine voor Azure Marketplace | Microsoft Docs
description: Inzicht en voer de stappen voor de installatiekopie van een lokale virtuele machine maken en implementeren in Azure Marketplace voor anderen om aan te schaffen.
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
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="50236-103">Een installatiekopie van een lokale virtuele machine ontwikkelen voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="50236-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="50236-104">Wij raden u aan Azure virtuele harde schijven (VHD's) rechtstreeks in de cloud te ontwikkelen met behulp van Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="50236-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="50236-105">Als u moet is het echter mogelijk te downloaden van een VHD en het ontwikkelen met behulp van on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="50236-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="50236-106">Voor lokale ontwikkeling, moet u de VHD van de gemaakte virtuele machine van het besturingssysteem downloaden.</span><span class="sxs-lookup"><span data-stu-id="50236-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="50236-107">Deze stappen zou worden uitgevoerd als onderdeel van de stap 3.3, hierboven.</span><span class="sxs-lookup"><span data-stu-id="50236-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="50236-108">Een VHD-installatiekopie te downloaden</span><span class="sxs-lookup"><span data-stu-id="50236-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="50236-109">Ga naar een blob-URL</span><span class="sxs-lookup"><span data-stu-id="50236-109">Locate a blob URL</span></span>
<span data-ttu-id="50236-110">Om te downloaden van de VHD, moet u eerst de blob-URL voor de besturingssysteemschijf vinden.</span><span class="sxs-lookup"><span data-stu-id="50236-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="50236-111">Zoek de blob-URL van de nieuwe [Microsoft Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="50236-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="50236-112">Ga naar **Bladeren** > **VMs**, en selecteer vervolgens de geïmplementeerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="50236-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="50236-113">Onder **configureren**, selecteer de **schijven** tegel, waarmee u de blade schijven opent.</span><span class="sxs-lookup"><span data-stu-id="50236-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="50236-115">Selecteer de **Besturingssysteemschijf**, die een andere blade die wordt weergegeven van de eigenschappen van de schijf, met inbegrip van de VHD-locatie wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="50236-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="50236-116">Kopieer deze blob-URL.</span><span class="sxs-lookup"><span data-stu-id="50236-116">Copy this blob URL.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="50236-118">Verwijder de geïmplementeerde virtuele machine nu zonder te verwijderen van de schijven van de back-ups maken.</span><span class="sxs-lookup"><span data-stu-id="50236-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="50236-119">U kunt ook stop de virtuele machine in plaats van te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="50236-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="50236-120">Download het VHD-besturingssysteem niet wanneer de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="50236-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="50236-122">Een VHD downloaden</span><span class="sxs-lookup"><span data-stu-id="50236-122">Download a VHD</span></span>
<span data-ttu-id="50236-123">Nadat u de URL van de blob weet, kunt u de VHD downloaden met behulp van de [Azure-portal](http://manage.windowsazure.com/) of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50236-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="50236-124">Op het moment van het maken van deze handleiding is de functionaliteit voor het downloaden van een VHD nog niet aanwezig in de nieuwe Microsoft Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="50236-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="50236-125">**Downloaden van het besturingssysteem-VHD via de huidige [Azure-portal](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="50236-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="50236-126">Meld u aan bij de Azure portal als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="50236-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="50236-127">Klik op de **opslag** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50236-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="50236-128">Selecteer het opslagaccount waarin de VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="50236-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="50236-130">U ziet nu eigenschappen van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50236-130">This displays storage account properties.</span></span> <span data-ttu-id="50236-131">Selecteer de **Containers** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50236-131">Select the **Containers** tab.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="50236-133">Selecteer de container waarin de VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="50236-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="50236-134">Standaard wordt de VHD opgeslagen in een VHD-container wanneer gemaakt vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="50236-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="50236-136">Selecteer het juiste besturingssysteem VHD door het vergelijken van de URL die u hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="50236-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="50236-137">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="50236-137">Click **Download**.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="50236-139">Een VHD te downloaden met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="50236-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="50236-140">Naast de Azure-portal gebruikt, kunt u de [opslaan AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet voor het downloaden van het besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="50236-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="50236-141">Bijvoorbeeld opslaan-AzureVhd-bron "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath 'C:\Users\Administrator\Desktop\baseimagevm.vhd' - StorageKey<String></span><span class="sxs-lookup"><span data-stu-id="50236-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="50236-142">**Opslaan AzureVhd** heeft ook een **NumberOfThreads** -optie die kan worden gebruikt voor het verhogen van parallelle uitvoering om optimaal gebruik van de beschikbare bandbreedte voor het downloaden.</span><span class="sxs-lookup"><span data-stu-id="50236-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="50236-143">VHD's uploaden naar Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="50236-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="50236-144">Als u uw VHD's on-premises voorbereid, moet u ze uploaden naar een opslagaccount in Azure.</span><span class="sxs-lookup"><span data-stu-id="50236-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="50236-145">Deze stap vindt plaats nadat het maken van uw VHD lokale maar voordat het verkrijgen van de certificeringsinstantie voor uw VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="50236-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="50236-146">Een opslagaccount en container maken</span><span class="sxs-lookup"><span data-stu-id="50236-146">Create a storage account and container</span></span>
<span data-ttu-id="50236-147">We raden aan dat de VHD's worden geüpload naar een opslagaccount in een regio in de Verenigde Staten.</span><span class="sxs-lookup"><span data-stu-id="50236-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="50236-148">Alle VHD's voor een enkele SKU worden geplaatst in een enkele container binnen een enkele opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50236-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="50236-149">Als u wilt een opslagaccount maakt, kunt u de [Microsoft Azure-portal](https://portal.azure.com/), PowerShell of de Linux-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="50236-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="50236-150">**Een opslagaccount maken vanuit de Microsoft Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="50236-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="50236-151">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="50236-151">Click **New**.</span></span>
2. <span data-ttu-id="50236-152">Selecteer **opslag**.</span><span class="sxs-lookup"><span data-stu-id="50236-152">Select **Storage**.</span></span>
3. <span data-ttu-id="50236-153">Vul de opslagaccountnaam en selecteer vervolgens een locatie.</span><span class="sxs-lookup"><span data-stu-id="50236-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="50236-155">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="50236-155">Click **Create**.</span></span>
5. <span data-ttu-id="50236-156">De blade voor het opslagaccount is geopend.</span><span class="sxs-lookup"><span data-stu-id="50236-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="50236-157">Zo niet, selecteer **Bladeren** > **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="50236-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="50236-158">Selecteer op de blade Opslagaccount, het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="50236-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="50236-159">Selecteer **Containers**.</span><span class="sxs-lookup"><span data-stu-id="50236-159">Select **Containers**.</span></span>
   
   ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="50236-161">Selecteer op de blade Containers **toevoegen**, en voer vervolgens een containernaam en de machtigingen van de container.</span><span class="sxs-lookup"><span data-stu-id="50236-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="50236-162">Selecteer **persoonlijke** voor machtigingen van de container.</span><span class="sxs-lookup"><span data-stu-id="50236-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="50236-163">U wordt aangeraden dat u maakt een container per SKU die u van plan bent om te publiceren.</span><span class="sxs-lookup"><span data-stu-id="50236-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![tekenen](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="50236-165">Een opslagaccount maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="50236-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="50236-166">Met behulp van PowerShell, een opslagaccount maken met behulp van de [nieuw AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50236-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="50236-167">Vervolgens u een container in dat storage-account maken met behulp van kunt de [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50236-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="50236-168">Deze opdrachten wordt ervan uitgegaan dat de huidige context van de storage-account is al ingesteld in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50236-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="50236-169">Raadpleeg [instellen van Azure PowerShell](marketplace-publishing-powershell-setup.md) voor meer informatie over de installatie van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50236-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="50236-170">Een opslagaccount maken met behulp van het opdrachtregelprogramma voor Mac en Linux</span><span class="sxs-lookup"><span data-stu-id="50236-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="50236-171">Van [Linux opdrachtregelprogramma](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), als volgt een opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="50236-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="50236-172">Als volgt te werk om een container te maken.</span><span class="sxs-lookup"><span data-stu-id="50236-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="50236-173">Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="50236-173">Upload a VHD</span></span>
<span data-ttu-id="50236-174">Nadat het opslagaccount en container zijn gemaakt, kunt u uw voorbereide VHD's uploaden.</span><span class="sxs-lookup"><span data-stu-id="50236-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="50236-175">U kunt PowerShell, het opdrachtregelprogramma Linux of andere Azure Storage management-hulpprogramma's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50236-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="50236-176">Een VHD via PowerShell uploaden</span><span class="sxs-lookup"><span data-stu-id="50236-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="50236-177">Gebruik de [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50236-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="50236-178">Een VHD uploaden met behulp van het opdrachtregelprogramma voor Mac en Linux</span><span class="sxs-lookup"><span data-stu-id="50236-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="50236-179">Met de [Linux opdrachtregelprogramma](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), gebruikt u de volgende: azure vm-installatiekopie maken <image name> --locatie <Location of the data center> --OS Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="50236-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="50236-180">Zie ook</span><span class="sxs-lookup"><span data-stu-id="50236-180">See also</span></span>
* [<span data-ttu-id="50236-181">De installatiekopie van een virtuele machine maken voor de Marketplace</span><span class="sxs-lookup"><span data-stu-id="50236-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="50236-182">Instellen van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="50236-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

