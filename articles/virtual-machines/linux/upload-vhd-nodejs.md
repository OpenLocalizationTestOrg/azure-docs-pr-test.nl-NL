---
title: een aangepaste installatiekopie Linux met Azure CLI 1.0 aaaUpload | Microsoft Docs
description: Maken en uploaden van een virtuele harde schijf (VHD) tooAzure met een aangepaste Linux-installatiekopie met Hallo Resource Manager-implementatiemodel en hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="845fa-103">Uploaden en Linux-VM maken van aangepaste installatiekopie met behulp van hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="845fa-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="845fa-104">Dit artikel ziet u hoe een virtuele harde schijf (VHD) tooAzure met tooupload Hallo Resource Manager-implementatiemodel en virtuele Linux-machines van deze aangepaste installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="845fa-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="845fa-105">Deze functionaliteit kunt u tooinstall en configureren van een Linux distro tooyour vereisten en gebruik vervolgens deze VHD tooquickly Azure virtuele machines (VM's) maken.</span><span class="sxs-lookup"><span data-stu-id="845fa-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="845fa-106">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="845fa-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="845fa-107">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="845fa-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="845fa-108">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="845fa-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="845fa-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="845fa-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="845fa-110">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="845fa-110">Quick commands</span></span>
<span data-ttu-id="845fa-111">Als u moet tooquickly Hallo taak, na de sectie details Hallo Hallo baseren opdrachten tooupload een tooAzure VM.</span><span class="sxs-lookup"><span data-stu-id="845fa-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="845fa-112">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#requirements).</span><span class="sxs-lookup"><span data-stu-id="845fa-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="845fa-113">Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="845fa-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="845fa-114">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="845fa-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="845fa-115">Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `myimages`.</span><span class="sxs-lookup"><span data-stu-id="845fa-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="845fa-116">Maak eerst een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="845fa-116">First, create a resource group.</span></span> <span data-ttu-id="845fa-117">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUs` locatie:</span><span class="sxs-lookup"><span data-stu-id="845fa-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="845fa-118">Een toohold storage-account van uw virtuele schijven maken.</span><span class="sxs-lookup"><span data-stu-id="845fa-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="845fa-119">Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="845fa-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="845fa-120">Lijst Hallo toegangssleutels voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="845fa-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="845fa-121">Maak een notitie van `key1`:</span><span class="sxs-lookup"><span data-stu-id="845fa-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="845fa-122">Maak een container in uw storage-account met behulp van Hallo-opslagsleutel die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="845fa-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="845fa-123">Hallo volgende voorbeeld wordt een container met de naam `myimages` met Hallo opslag sleutelwaarde van `key1`:</span><span class="sxs-lookup"><span data-stu-id="845fa-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="845fa-124">Ten slotte upload uw VHD toohello-container die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="845fa-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="845fa-125">Geef Hallo lokaal pad tooyour VHD onder `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="845fa-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="845fa-126">U kunt nu een virtuele machine maken van de geüploade virtuele schijf [met een Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="845fa-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="845fa-127">U kunt ook Hallo CLI door Hallo URI tooyour schijf opgeven (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="845fa-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="845fa-128">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` gebruik van de virtuele schijf Hallo eerder hebt geüpload:</span><span class="sxs-lookup"><span data-stu-id="845fa-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="845fa-129">Hallo doelopslagaccount heeft toobe Hallo dezelfde als waar u de virtuele schijf geüpload.</span><span class="sxs-lookup"><span data-stu-id="845fa-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="845fa-130">Of u kunt ook toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo `azure vm create` opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="845fa-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="845fa-131">U kunt meer lezen over Hallo [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="845fa-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="845fa-132">Vereisten</span><span class="sxs-lookup"><span data-stu-id="845fa-132">Requirements</span></span>
<span data-ttu-id="845fa-133">Hallo toocomplete volgende stappen die u nodig:</span><span class="sxs-lookup"><span data-stu-id="845fa-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="845fa-134">**Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -installeren van een [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in VHD Hallo de indeling.</span><span class="sxs-lookup"><span data-stu-id="845fa-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="845fa-135">Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:</span><span class="sxs-lookup"><span data-stu-id="845fa-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="845fa-136">Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling.</span><span class="sxs-lookup"><span data-stu-id="845fa-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="845fa-137">Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="845fa-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="845fa-138">U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="845fa-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="845fa-139">Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="845fa-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="845fa-140">Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling.</span><span class="sxs-lookup"><span data-stu-id="845fa-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="845fa-141">Indien nodig, kunt u converteren VHDX schijven tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="845fa-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="845fa-142">Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="845fa-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="845fa-143">U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="845fa-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="845fa-144">Virtuele machines die zijn gemaakt op basis van uw aangepaste installatiekopie moeten zich bevinden in Hallo hetzelfde opslagaccount als Hallo installatiekopie zelf</span><span class="sxs-lookup"><span data-stu-id="845fa-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="845fa-145">Maken van een storage-account en de container toohold uw aangepaste installatiekopie en de gemaakte virtuele machines</span><span class="sxs-lookup"><span data-stu-id="845fa-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="845fa-146">Nadat u uw virtuele machines hebt gemaakt, kunt u veilig uw installatiekopie verwijderen</span><span class="sxs-lookup"><span data-stu-id="845fa-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="845fa-147">Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="845fa-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="845fa-148">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="845fa-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="845fa-149">Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `myimages`.</span><span class="sxs-lookup"><span data-stu-id="845fa-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="845fa-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="845fa-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="845fa-151">Hallo installatiekopie toobe geüpload voorbereiden</span><span class="sxs-lookup"><span data-stu-id="845fa-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="845fa-152">Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="845fa-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="845fa-153">Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund op Azure:</span><span class="sxs-lookup"><span data-stu-id="845fa-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="845fa-154">**[Op basis van centOS distributies](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="845fa-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="845fa-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="845fa-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="845fa-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="845fa-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="845fa-160">**[Andere - niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="845fa-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="845fa-161">Zie ook Hallo  **[opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="845fa-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="845fa-162">Hallo [Azure-platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) is van toepassing tooVMs met Linux alleen met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' wanneer een van de Hallo goedgekeurde distributies wordt gebruikt in [Linux op door Azure goedgekeurde Distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="845fa-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="845fa-163">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="845fa-163">Create a resource group</span></span>
<span data-ttu-id="845fa-164">Resourcegroepen samenbrengen logisch alle hello Azure-resources toosupport uw virtuele machines, zoals Hallo virtuele netwerken en opslag.</span><span class="sxs-lookup"><span data-stu-id="845fa-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="845fa-165">Lees meer over [Azure resourcegroepen hier](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="845fa-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="845fa-166">Voordat u uw aangepaste schijfimage uploaden en het maken van virtuele machines, moet u eerst toocreate een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="845fa-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="845fa-167">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUS` locatie:</span><span class="sxs-lookup"><span data-stu-id="845fa-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="845fa-168">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="845fa-168">Create a storage account</span></span>
<span data-ttu-id="845fa-169">Virtuele machines worden opgeslagen als pagina-blobs binnen een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="845fa-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="845fa-170">Lees meer over [hier Azure blob-opslag](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="845fa-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="845fa-171">U maken een opslagaccount voor uw aangepaste schijfimage en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="845fa-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="845fa-172">Alle virtuele machines die u maakt van uw aangepaste schijf installatiekopie moeten toobe in Hallo hetzelfde opslagaccount als installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="845fa-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="845fa-173">Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount` in de resourcegroep Hallo eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="845fa-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="845fa-174">Lijst met sleutels voor opslagaccount</span><span class="sxs-lookup"><span data-stu-id="845fa-174">List storage account keys</span></span>
<span data-ttu-id="845fa-175">Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert.</span><span class="sxs-lookup"><span data-stu-id="845fa-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="845fa-176">Deze toegangstoetsen worden gebruikt bij het verifiëren van toohello storage-account, zoals toocarry uit schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="845fa-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="845fa-177">Lees meer over [het beheren van toegang tot toostorage hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="845fa-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="845fa-178">U kunt toegangstoetsen Hello weergeven `azure storage account keys list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="845fa-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="845fa-179">Weergave Hallo toegangstoetsen voor Hallo storage-account die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="845fa-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="845fa-180">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="845fa-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="845fa-181">Maak een notitie van `key1` terwijl u met deze toointeract met uw opslagaccount in de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="845fa-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="845fa-182">Een opslagcontainer maken</span><span class="sxs-lookup"><span data-stu-id="845fa-182">Create a storage container</span></span>
<span data-ttu-id="845fa-183">In Hallo indelen dezelfde manier waarop u verschillende mappen toologically het lokale bestandssysteem, maakt u containers in een storage account tooorganize uw virtuele schijven en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="845fa-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="845fa-184">Een opslagaccount kan een onbeperkt aantal containers bevatten.</span><span class="sxs-lookup"><span data-stu-id="845fa-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="845fa-185">Hallo volgende voorbeeld wordt een container met de naam `myimages`, in de vorige stap Hallo Hallo toegangssleutel geven verkregen (`key1`):</span><span class="sxs-lookup"><span data-stu-id="845fa-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="845fa-186">Virtuele harde schijf geüpload</span><span class="sxs-lookup"><span data-stu-id="845fa-186">Upload VHD</span></span>
<span data-ttu-id="845fa-187">Nu kunt u uw aangepaste schijfimage daadwerkelijk uploaden.</span><span class="sxs-lookup"><span data-stu-id="845fa-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="845fa-188">Als met alle virtuele schijven die door virtuele machines, gebruikt u uploaden en uw aangepaste schijfimage opslaan als een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="845fa-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="845fa-189">Geef uw toegangssleutel, Hallo-container die u hebt gemaakt in de vorige stap Hallo en vervolgens Hallo pad toohello aangepaste schijfimage op uw lokale computer:</span><span class="sxs-lookup"><span data-stu-id="845fa-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="845fa-190">Virtuele machine van de aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="845fa-190">Create VM from custom image</span></span>
<span data-ttu-id="845fa-191">Wanneer u virtuele machines van de installatiekopie van uw aangepaste schijf maakt, geef Hallo URI toohello schijfimage.</span><span class="sxs-lookup"><span data-stu-id="845fa-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="845fa-192">Zorg ervoor dat Hallo bestemming storage-account komt overeen met waar de installatiekopie van uw aangepaste schijf wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="845fa-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="845fa-193">U kunt uw virtuele machine met behulp van hello Azure CLI of Resource Manager JSON-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="845fa-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="845fa-194">Een virtuele machine maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="845fa-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="845fa-195">Geef van Hallo `--image-urn` parameter Hello `azure vm create` opdracht toopoint tooyour aangepaste schijfimage.</span><span class="sxs-lookup"><span data-stu-id="845fa-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="845fa-196">Zorg ervoor dat `--storage-account-name` komt overeen met Hallo opslagaccount waarin de installatiekopie van uw aangepaste schijf wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="845fa-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="845fa-197">U beschikt niet over toouse Hallo dezelfde container als aangepaste schijf installatiekopie toostore Hallo uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="845fa-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="845fa-198">Zorg ervoor dat toocreate andere containers in Hallo dezelfde manier als Hallo eerdere stappen voordat u uw aangepaste schijfkopieën uploadt.</span><span class="sxs-lookup"><span data-stu-id="845fa-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="845fa-199">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` van uw aangepaste schijfimage:</span><span class="sxs-lookup"><span data-stu-id="845fa-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="845fa-200">Of u kunt nog steeds toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo `azure vm create` opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="845fa-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="845fa-201">Lees meer over Hallo [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="845fa-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="845fa-202">Een virtuele machine met een JSON-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="845fa-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="845fa-203">Azure Resource Manager-sjablonen zijn JSON JavaScript Object Notation ()-bestanden die u wenst dat toobuild Hallo-omgeving definiëren.</span><span class="sxs-lookup"><span data-stu-id="845fa-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="845fa-204">Hallo-sjablonen zijn onderverdeeld in de resourceproviders toodifferent zoals compute of een netwerk.</span><span class="sxs-lookup"><span data-stu-id="845fa-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="845fa-205">U kunt bestaande sjablonen gebruiken of uw eigen schrijven.</span><span class="sxs-lookup"><span data-stu-id="845fa-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="845fa-206">Lees meer over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="845fa-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="845fa-207">Binnen Hallo `Microsoft.Compute/virtualMachines` provider van de sjabloon die u hebt een `storageProfile` knooppunt met Hallo configuratiedetails voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="845fa-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="845fa-208">Hallo twee belangrijkste parameters tooedit zijn Hallo `image` en `vhd` URI's die verwijzen tooyour aangepaste installatiekopie en de virtuele schijf van de nieuwe VM.</span><span class="sxs-lookup"><span data-stu-id="845fa-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="845fa-209">Hallo hieronder toont een voorbeeld van Hallo JSON voor het gebruik van een aangepaste installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="845fa-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="845fa-210">U kunt [deze bestaande sjabloon toocreate een virtuele machine van een aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) of lezen over [maken van uw eigen Azure Resource Manager-sjablonen](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="845fa-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="845fa-211">Zodra u een sjabloon die is geconfigureerd hebt, hebt u uw virtuele machines met behulp van Hallo `azure group deployment create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="845fa-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="845fa-212">Hallo-URI van de JSON-sjabloon opgeven met Hallo `--template-uri` parameter:</span><span class="sxs-lookup"><span data-stu-id="845fa-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="845fa-213">Als u een JSON-bestand die lokaal zijn opgeslagen op uw computer hebt, kunt u Hallo `--template-file` parameter in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="845fa-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="845fa-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="845fa-214">Next steps</span></span>
<span data-ttu-id="845fa-215">Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="845fa-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="845fa-216">U kunt ook te[een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nieuwe virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="845fa-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="845fa-217">Als u toepassingen die worden uitgevoerd op uw virtuele machines dat u tooaccess nodig hebt, moet u te[openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="845fa-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

