---
title: aaaCreate en een tooAzure Linux VHD uploaden | Microsoft Docs
description: Maken en uploaden van een Azure virtuele harde schijf (VHD) die Hallo Linux-besturingssysteem met behulp van Hallo klassieke implementatiemodel bevat
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
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="310dd-103">Maakt en uploadt u een virtuele harde schijf met Hallo Linux-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="310dd-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="310dd-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="310dd-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="310dd-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="310dd-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="310dd-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="310dd-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="310dd-107">U kunt ook [uploaden van een aangepaste installatiekopie met Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="310dd-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="310dd-108">Dit artikel laat zien hoe toocreate en het uploaden van een virtuele harde schijf (VHD) zodat u deze als uw eigen gebruiken kunt installatiekopie toocreate virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="310dd-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="310dd-109">Meer informatie over hoe tooprepare Hallo besturingssysteem zodat u deze, kunt u toocreate gebruiken kunt meerdere virtuele machines op basis van die installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="310dd-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="310dd-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="310dd-110">Prerequisites</span></span>
<span data-ttu-id="310dd-111">In dit artikel wordt ervan uitgegaan dat u hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="310dd-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="310dd-112">**Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -u hebt geïnstalleerd een [door Azure goedgekeurde Linux-distributie](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in Hallo VHD-indeling.</span><span class="sxs-lookup"><span data-stu-id="310dd-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="310dd-113">Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:</span><span class="sxs-lookup"><span data-stu-id="310dd-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="310dd-114">Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling.</span><span class="sxs-lookup"><span data-stu-id="310dd-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="310dd-115">Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="310dd-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="310dd-116">U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="310dd-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="310dd-117">Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="310dd-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="310dd-118">Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling.</span><span class="sxs-lookup"><span data-stu-id="310dd-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="310dd-119">Indien nodig, kunt u converteren VHDX schijven tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="310dd-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="310dd-120">Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="310dd-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="310dd-121">U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="310dd-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="310dd-122">**Azure-opdrachtregelinterface** -meest recente installatie Hallo [Azure-opdrachtregelinterface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="310dd-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="310dd-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="310dd-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="310dd-124">Stap 1: Voorbereiden Hallo installatiekopie toobe geüpload</span><span class="sxs-lookup"><span data-stu-id="310dd-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="310dd-125">Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="310dd-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="310dd-126">Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="310dd-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="310dd-127">Nadat u de stappen in de volgende handleidingen Hallo Hallo hebt voltooid, kun je hier als u een VHD-bestand dat is gereed tooupload tooAzure hebt:</span><span class="sxs-lookup"><span data-stu-id="310dd-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="310dd-128">**[Op basis van centOS distributies](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="310dd-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="310dd-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="310dd-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="310dd-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="310dd-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="310dd-134">**[Andere - niet-goedgekeurde distributies](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="310dd-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="310dd-135">Hello Azure-platform SLA van toepassing is toovirtual machines met Linux-besturingssysteem alleen als een van de Hallo distributies goedgekeurde wordt gebruikt met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' hello in [Linux op Azure-Endorsed distributies ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="310dd-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="310dd-136">Alle Linux-distributies in de afbeelding voor Azure-galerie Hallo zijn aangebracht distributies met Hallo vereiste configuratie.</span><span class="sxs-lookup"><span data-stu-id="310dd-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="310dd-137">Zie ook Hallo  **[opmerkingen bij de installatie van Linux](../create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="310dd-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="310dd-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="310dd-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="310dd-139">Stap 2: Hallo verbinding tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="310dd-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="310dd-140">Zorg ervoor dat u gebruikmaakt van hello Azure CLI in het klassieke implementatiemodel hello (`azure config mode asm`), meld u daarna tooyour account:</span><span class="sxs-lookup"><span data-stu-id="310dd-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="310dd-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="310dd-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="310dd-142">Stap 3: Hallo installatiekopie tooAzure uploaden</span><span class="sxs-lookup"><span data-stu-id="310dd-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="310dd-143">U moet uw VHD-bestand naar een tooupload storage-account.</span><span class="sxs-lookup"><span data-stu-id="310dd-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="310dd-144">Kunt u een bestaand opslagaccount kiezen of [Maak een nieuwe](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="310dd-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="310dd-145">Hello Azure CLI tooupload Hallo installatiekopie door Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="310dd-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="310dd-146">In het vorige voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="310dd-146">In hello previous example:</span></span>

* <span data-ttu-id="310dd-147">**BlobStorageURL** Hallo-URL voor Hallo u van plan bent toouse storage-account</span><span class="sxs-lookup"><span data-stu-id="310dd-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="310dd-148">**YourImagesFolder** Hallo-container in blob-opslag is waar u toostore uw installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="310dd-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="310dd-149">**VHDName** Hallo-label die wordt weergegeven in de portal tooidentify Hallo virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="310dd-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="310dd-150">**PathToVHDFile** Hallo volledig pad en naam van Hallo .vhd-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="310dd-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="310dd-151">Hallo na de opdracht ziet u een compleet voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="310dd-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="310dd-152">Stap 4: Een virtuele machine uit Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="310dd-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="310dd-153">U maakt een virtuele machine met `azure vm create` in Hallo dezelfde manier als een gewone virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="310dd-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="310dd-154">Hebt u uw installatiekopie gegeven in de vorige stap Hallo Hallo-naam opgeven.</span><span class="sxs-lookup"><span data-stu-id="310dd-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="310dd-155">In de Hallo voorbeeld te volgen, gebruiken we Hallo **myImage** de naam van de installatiekopie is opgegeven in de vorige stap Hallo:</span><span class="sxs-lookup"><span data-stu-id="310dd-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="310dd-156">toocreate uw eigen virtuele machines, Geef uw eigen gebruikersnaam en wachtwoord, locatie, DNS-naam en installatiekopie met de naam.</span><span class="sxs-lookup"><span data-stu-id="310dd-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="310dd-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="310dd-157">Next steps</span></span>
<span data-ttu-id="310dd-158">Zie voor meer informatie [Azure CLI-verwijzing voor hello Azure klassieke implementatiemodel](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="310dd-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
