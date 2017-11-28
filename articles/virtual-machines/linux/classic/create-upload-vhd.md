---
title: Maken en een Linux-VHD uploaden naar Azure | Microsoft Docs
description: Maken en uploaden van een Azure virtuele harde schijf (VHD) met het Linux-besturingssysteem met behulp van het klassieke implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 23c30c954875598ce3e01db137b0ef8cda9779f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-the-linux-operating-system"></a><span data-ttu-id="280ec-103">Een virtuele harde schijf met het Linux-besturingssysteem maken en uploaden</span><span class="sxs-lookup"><span data-stu-id="280ec-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="280ec-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="280ec-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="280ec-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="280ec-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="280ec-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="280ec-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="280ec-107">U kunt ook [uploaden van een aangepaste installatiekopie met Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="280ec-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="280ec-108">In dit artikel leest u hoe maken en uploaden van een virtuele harde schijf (VHD), zodat u deze als uw eigen installatiekopie gebruiken kunt maken van virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="280ec-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span></span> <span data-ttu-id="280ec-109">Informatie over het voorbereiden van het besturingssysteem, zodat u deze gebruiken kunt voor het maken van meerdere virtuele machines op basis van die installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="280ec-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="280ec-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="280ec-110">Prerequisites</span></span>
<span data-ttu-id="280ec-111">In dit artikel wordt ervan uitgegaan dat u de volgende items hebt:</span><span class="sxs-lookup"><span data-stu-id="280ec-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="280ec-112">**Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -u hebt geïnstalleerd een [door Azure goedgekeurde Linux-distributie](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) naar een virtuele schijf in de VHD-indeling.</span><span class="sxs-lookup"><span data-stu-id="280ec-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="280ec-113">Er bestaan meerdere hulpprogramma's om een virtuele machine en de VHD te maken:</span><span class="sxs-lookup"><span data-stu-id="280ec-113">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="280ec-114">Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), zorg ervoor dat de VHD gebruiken als uw afbeeldingsindeling.</span><span class="sxs-lookup"><span data-stu-id="280ec-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="280ec-115">Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="280ec-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="280ec-116">U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="280ec-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="280ec-117">De nieuwe VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="280ec-117">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="280ec-118">Wanneer u een virtuele machine maakt, geeft u de VHD als de notatie.</span><span class="sxs-lookup"><span data-stu-id="280ec-118">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="280ec-119">Indien nodig, kunt u de VHDX-schijven converteren naar VHD gebruiken [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of de [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="280ec-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="280ec-120">Azure biedt bovendien geen ondersteuning dynamische VHD's uploaden, dus u deze schijven worden geconverteerd naar vaste VHD's moet voordat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="280ec-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="280ec-121">U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) naar dynamische schijven converteren tijdens het proces van het uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="280ec-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>

* <span data-ttu-id="280ec-122">**Azure-opdrachtregelinterface** -Installeer de meest recente [Azure-opdrachtregelinterface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) om de VHD te uploaden.</span><span class="sxs-lookup"><span data-stu-id="280ec-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span></span>

<span data-ttu-id="280ec-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="280ec-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-the-image-to-be-uploaded"></a><span data-ttu-id="280ec-124">Stap 1: Bereid de afbeelding die moet worden geüpload</span><span class="sxs-lookup"><span data-stu-id="280ec-124">Step 1: Prepare the image to be uploaded</span></span>
<span data-ttu-id="280ec-125">Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="280ec-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="280ec-126">De volgende artikelen helpen u bij het voorbereiden van de verschillende Linux-distributies die worden ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="280ec-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="280ec-127">Nadat u de stappen in de volgende handleidingen hebt voltooid, kun je hier als u een VHD-bestand dat is gereed om te uploaden naar Azure hebt:</span><span class="sxs-lookup"><span data-stu-id="280ec-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span></span>

* <span data-ttu-id="280ec-128">**[Op basis van centOS distributies](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="280ec-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="280ec-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="280ec-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="280ec-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="280ec-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="280ec-134">**[Andere - niet-goedgekeurde distributies](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="280ec-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="280ec-135">De Azure-platform SLA van toepassing op virtuele machines met Linux-besturingssysteem alleen als een van de aangebracht distributies wordt gebruikt met de configuratie van de gegevens zoals opgegeven in de ondersteunde versies' in [Linux op Azure-Endorsed distributies](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="280ec-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="280ec-136">Alle Linux-distributies in de afbeelding voor Azure-galerie zijn aangebracht distributies en de vereiste configuratie.</span><span class="sxs-lookup"><span data-stu-id="280ec-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span></span>
> 
> 

<span data-ttu-id="280ec-137">Zie ook de  **[opmerkingen bij de installatie van Linux](../create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="280ec-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="280ec-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="280ec-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-the-connection-to-azure"></a><span data-ttu-id="280ec-139">Stap 2: De verbinding met Azure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="280ec-139">Step 2: Prepare the connection to Azure</span></span>
<span data-ttu-id="280ec-140">Controleer of u de Azure CLI in het klassieke implementatiemodel (`azure config mode asm`), meld u vervolgens aan bij uw account:</span><span class="sxs-lookup"><span data-stu-id="280ec-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="280ec-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="280ec-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-the-image-to-azure"></a><span data-ttu-id="280ec-142">Stap 3: De installatiekopie uploaden naar Azure</span><span class="sxs-lookup"><span data-stu-id="280ec-142">Step 3: Upload the image to Azure</span></span>
<span data-ttu-id="280ec-143">U moet een opslagaccount voor uw VHD-bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="280ec-143">You need a storage account to upload your VHD file to.</span></span> <span data-ttu-id="280ec-144">Kunt u een bestaand opslagaccount kiezen of [Maak een nieuwe](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="280ec-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="280ec-145">De Azure CLI gebruiken voor het uploaden van de installatiekopie met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="280ec-145">Use the Azure CLI to upload the image by using the following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="280ec-146">In het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="280ec-146">In the previous example:</span></span>

* <span data-ttu-id="280ec-147">**BlobStorageURL** is de URL voor het opslagaccount dat u wilt gebruiken</span><span class="sxs-lookup"><span data-stu-id="280ec-147">**BlobStorageURL** is the URL for the storage account you plan to use</span></span>
* <span data-ttu-id="280ec-148">**YourImagesFolder** is een container in blob storage waar u uw installatiekopieën opslaan</span><span class="sxs-lookup"><span data-stu-id="280ec-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span></span>
* <span data-ttu-id="280ec-149">**VHDName** wordt het label dat wordt weergegeven in de portal voor het identificeren van de virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="280ec-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="280ec-150">**PathToVHDFile** is het volledige pad en de naam van het VHD-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="280ec-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span></span>

<span data-ttu-id="280ec-151">Een compleet voorbeeld ziet u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="280ec-151">The following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-the-image"></a><span data-ttu-id="280ec-152">Stap 4: Een virtuele machine van de installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="280ec-152">Step 4: Create a VM from the image</span></span>
<span data-ttu-id="280ec-153">U maakt een virtuele machine met `azure vm create` op dezelfde manier als een gewone virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="280ec-153">You create a VM using `azure vm create` in the same way as a regular VM.</span></span> <span data-ttu-id="280ec-154">Geef de naam die u hebt uw installatiekopie gegeven in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="280ec-154">Specify the name you gave your image in the previous step.</span></span> <span data-ttu-id="280ec-155">In het volgende voorbeeld gebruiken we de **myImage** de naam van de installatiekopie is opgegeven in de vorige stap:</span><span class="sxs-lookup"><span data-stu-id="280ec-155">In the following example, we use the **myImage** image name given in the previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="280ec-156">Geef uw eigen gebruikersnaam en wachtwoord, locatie, DNS-naam en installatiekopie met de naam voor het maken van uw eigen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="280ec-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="280ec-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="280ec-157">Next steps</span></span>
<span data-ttu-id="280ec-158">Zie voor meer informatie [Azure CLI-verwijzing voor het klassieke implementatiemodel Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="280ec-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare the image to be uploaded]:#prepimage
[Step 2: Prepare the connection to Azure]:#connect
[Step 3: Upload the image to Azure]:#upload
