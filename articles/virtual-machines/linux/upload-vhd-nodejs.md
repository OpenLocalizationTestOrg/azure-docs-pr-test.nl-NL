---
title: Uploaden van een aangepaste installatiekopie Linux met Azure CLI 1.0 | Microsoft Docs
description: Maken en uploaden van een virtuele harde schijf (VHD) naar Azure met een aangepaste Linux-installatiekopie met behulp van het implementatiemodel van Resource Manager en de Azure CLI 1.0.
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
ms.openlocfilehash: ca4c6cb9296028275b2b032af0c94baabeec1223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="32077-103">Uploaden en een Linux-VM uit aangepaste installatiekopie maken met behulp van de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="32077-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="32077-104">In dit artikel laat zien hoe een virtuele harde schijf (VHD) uploaden naar Azure met behulp van het Resource Manager-implementatiemodel en virtuele Linux-machines van deze aangepaste installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="32077-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="32077-105">Deze functie kunt u installeren en configureren van een Linux-distro aan uw vereisten en gebruik vervolgens deze VHD snel virtuele Azure-machines (VM's) maken.</span><span class="sxs-lookup"><span data-stu-id="32077-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="32077-106">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="32077-106">CLI versions to complete the task</span></span>
<span data-ttu-id="32077-107">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="32077-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="32077-108">[Azure CLI 1.0](#quick-commands) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="32077-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="32077-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="32077-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="32077-110">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="32077-110">Quick commands</span></span>
<span data-ttu-id="32077-111">Als u nodig hebt voor de taak, de volgende sectie details snel de base-opdrachten voor het uploaden van een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="32077-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="32077-112">Meer gedetailleerde informatie en context voor elke stap u de rest van het document vindt [vanaf hier](#requirements).</span><span class="sxs-lookup"><span data-stu-id="32077-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="32077-113">Zorg ervoor dat u hebt [de Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="32077-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="32077-114">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="32077-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="32077-115">Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `myimages`.</span><span class="sxs-lookup"><span data-stu-id="32077-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="32077-116">Maak eerst een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="32077-116">First, create a resource group.</span></span> <span data-ttu-id="32077-117">Het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` in de `WestUs` locatie:</span><span class="sxs-lookup"><span data-stu-id="32077-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="32077-118">Een opslagaccount voor het opslaan van uw virtuele schijven maken.</span><span class="sxs-lookup"><span data-stu-id="32077-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="32077-119">Het volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="32077-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="32077-120">Lijst van de toegangssleutels voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="32077-120">List the access keys for your storage account.</span></span> <span data-ttu-id="32077-121">Maak een notitie van `key1`:</span><span class="sxs-lookup"><span data-stu-id="32077-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="32077-122">Maak een container in uw storage-account met de opslagsleutel die u hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="32077-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="32077-123">Het volgende voorbeeld wordt een container met de naam `myimages` met behulp van de opslag-sleutelwaarde van `key1`:</span><span class="sxs-lookup"><span data-stu-id="32077-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="32077-124">Ten slotte uw harde schijf geüpload naar de container die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="32077-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="32077-125">Geef het lokale pad naar uw VHD onder `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="32077-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="32077-126">U kunt nu een virtuele machine maken van de geüploade virtuele schijf [met een Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="32077-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="32077-127">U kunt ook de CLI gebruiken door op te geven van de URI naar de schijf (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="32077-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="32077-128">Het volgende voorbeeld wordt een virtuele machine met de naam `myVM` eerder met behulp van de virtuele schijf geüpload:</span><span class="sxs-lookup"><span data-stu-id="32077-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="32077-129">Het doelopslagaccount moet hetzelfde zijn als waarnaar u de virtuele schijf geüpload.</span><span class="sxs-lookup"><span data-stu-id="32077-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="32077-130">U moet ook opgeven of antwoord vraagt, alle extra parameters die zijn vereist voor de `azure vm create` opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="32077-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="32077-131">U kunt meer lezen over de [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="32077-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="32077-132">Vereisten</span><span class="sxs-lookup"><span data-stu-id="32077-132">Requirements</span></span>
<span data-ttu-id="32077-133">De volgende stappen uit te voeren, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="32077-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="32077-134">**Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -installeren van een [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) naar een virtuele schijf in de VHD-indeling.</span><span class="sxs-lookup"><span data-stu-id="32077-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="32077-135">Er bestaan meerdere hulpprogramma's om een virtuele machine en de VHD te maken:</span><span class="sxs-lookup"><span data-stu-id="32077-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="32077-136">Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), zorg ervoor dat de VHD gebruiken als uw afbeeldingsindeling.</span><span class="sxs-lookup"><span data-stu-id="32077-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="32077-137">Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="32077-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="32077-138">U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="32077-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="32077-139">De nieuwe VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="32077-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="32077-140">Wanneer u een virtuele machine maakt, geeft u de VHD als de notatie.</span><span class="sxs-lookup"><span data-stu-id="32077-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="32077-141">Indien nodig, kunt u de VHDX-schijven converteren naar VHD gebruiken [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of de [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32077-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="32077-142">Azure biedt bovendien geen ondersteuning dynamische VHD's uploaden, dus u deze schijven worden geconverteerd naar vaste VHD's moet voordat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="32077-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="32077-143">U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) naar dynamische schijven converteren tijdens het proces van het uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="32077-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="32077-144">Virtuele machines die zijn gemaakt op basis van uw aangepaste installatiekopie moeten zich bevinden in hetzelfde opslagaccount als de afbeelding zelf</span><span class="sxs-lookup"><span data-stu-id="32077-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="32077-145">Een opslagaccount en container voor het opslaan van uw aangepaste installatiekopie en de gemaakte virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="32077-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="32077-146">Nadat u uw virtuele machines hebt gemaakt, kunt u veilig uw installatiekopie verwijderen</span><span class="sxs-lookup"><span data-stu-id="32077-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="32077-147">Zorg ervoor dat u hebt [de Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:</span><span class="sxs-lookup"><span data-stu-id="32077-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="32077-148">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="32077-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="32077-149">Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `myimages`.</span><span class="sxs-lookup"><span data-stu-id="32077-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="32077-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="32077-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="32077-151">Voorbereiden van de afbeelding die moet worden geüpload</span><span class="sxs-lookup"><span data-stu-id="32077-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="32077-152">Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="32077-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="32077-153">De volgende artikelen helpt u bij het voorbereiden van de verschillende Linux-distributies die worden ondersteund op Azure:</span><span class="sxs-lookup"><span data-stu-id="32077-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="32077-154">**[Op basis van centOS distributies](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="32077-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="32077-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="32077-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="32077-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="32077-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="32077-160">**[Andere - niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="32077-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="32077-161">Zie ook de  **[opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="32077-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="32077-162">De [Azure-platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) is van toepassing op virtuele machines met Linux alleen als een van de aangebracht distributies wordt gebruikt met configuratiegegevens van de opgegeven onder ondersteunde versies' in [Linux op Azure-Endorsed distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32077-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="32077-163">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="32077-163">Create a resource group</span></span>
<span data-ttu-id="32077-164">Resourcegroepen samenbrengen logisch alle Azure-resources voor de ondersteuning van uw virtuele machines, zoals de virtuele netwerken en opslag.</span><span class="sxs-lookup"><span data-stu-id="32077-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="32077-165">Lees meer over [Azure resourcegroepen hier](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32077-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="32077-166">Voordat u uw aangepaste schijfimage uploaden en het maken van virtuele machines, moet u eerst een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="32077-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="32077-167">Het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` in de `WestUS` locatie:</span><span class="sxs-lookup"><span data-stu-id="32077-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="32077-168">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="32077-168">Create a storage account</span></span>
<span data-ttu-id="32077-169">Virtuele machines worden opgeslagen als pagina-blobs binnen een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="32077-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="32077-170">Lees meer over [hier Azure blob-opslag](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="32077-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="32077-171">U maken een opslagaccount voor uw aangepaste schijfimage en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="32077-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="32077-172">Alle virtuele machines die u van uw aangepaste schijfimage maakt moeten zich in hetzelfde opslagaccount als installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="32077-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="32077-173">Het volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount` in de resourcegroep die eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="32077-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="32077-174">Lijst met sleutels voor opslagaccount</span><span class="sxs-lookup"><span data-stu-id="32077-174">List storage account keys</span></span>
<span data-ttu-id="32077-175">Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert.</span><span class="sxs-lookup"><span data-stu-id="32077-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="32077-176">Deze toegangstoetsen worden gebruikt bij het verifiëren van de storage-account, zoals bij het uitvoeren van schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="32077-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="32077-177">Lees meer over [het beheren van toegang tot opslag hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="32077-177">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="32077-178">Vindt u sneltoetsen met de `azure storage account keys list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="32077-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="32077-179">Bekijk de toegangssleutels voor het opslagaccount dat u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="32077-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="32077-180">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="32077-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="32077-181">Maak een notitie van `key1` terwijl u deze wordt gebruikt om te communiceren met uw opslagaccount in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="32077-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="32077-182">Een opslagcontainer maken</span><span class="sxs-lookup"><span data-stu-id="32077-182">Create a storage container</span></span>
<span data-ttu-id="32077-183">Op dezelfde manier als u andere mappen maken om maken het lokale bestandssysteem logische manier te organiseren, maakt u containers in een opslagaccount voor het ordenen van uw virtuele schijven en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="32077-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="32077-184">Een opslagaccount kan een onbeperkt aantal containers bevatten.</span><span class="sxs-lookup"><span data-stu-id="32077-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="32077-185">Het volgende voorbeeld wordt een container met de naam `myimages`, geven de toegangssleutel in de vorige stap hebt verkregen (`key1`):</span><span class="sxs-lookup"><span data-stu-id="32077-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="32077-186">Virtuele harde schijf geüpload</span><span class="sxs-lookup"><span data-stu-id="32077-186">Upload VHD</span></span>
<span data-ttu-id="32077-187">Nu kunt u uw aangepaste schijfimage daadwerkelijk uploaden.</span><span class="sxs-lookup"><span data-stu-id="32077-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="32077-188">Als met alle virtuele schijven die door virtuele machines, gebruikt u uploaden en uw aangepaste schijfimage opslaan als een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="32077-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="32077-189">Geef uw toegangssleutel, voor de container die u hebt gemaakt in de vorige stap en het pad naar het aangepaste schijfimage op uw lokale computer:</span><span class="sxs-lookup"><span data-stu-id="32077-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="32077-190">Virtuele machine van de aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="32077-190">Create VM from custom image</span></span>
<span data-ttu-id="32077-191">Wanneer u virtuele machines van de installatiekopie van uw aangepaste schijf maakt, geeft u de URI op de schijfinstallatiekopie van de.</span><span class="sxs-lookup"><span data-stu-id="32077-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="32077-192">Zorg ervoor dat de bestemming storage-account komt overeen met waar de installatiekopie van uw aangepaste schijf wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="32077-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="32077-193">U kunt uw virtuele machine met de Azure CLI of Resource Manager JSON-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="32077-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="32077-194">Een virtuele machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="32077-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="32077-195">U geeft de `--image-urn` parameter met de `azure vm create` opdracht uit om te verwijzen naar de schijfinstallatiekopie van uw aangepaste.</span><span class="sxs-lookup"><span data-stu-id="32077-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="32077-196">Zorg ervoor dat `--storage-account-name` overeenkomt met het opslagaccount waar de installatiekopie van uw aangepaste schijf wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="32077-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="32077-197">U beschikt niet over dezelfde container gebruiken als de aangepaste schijfimage voor het opslaan van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="32077-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="32077-198">Zorg ervoor dat eventuele extra containers maken in dezelfde manier als de eerdere stappen voordat u uw aangepaste schijfkopieën uploadt.</span><span class="sxs-lookup"><span data-stu-id="32077-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="32077-199">Het volgende voorbeeld wordt een virtuele machine met de naam `myVM` van uw aangepaste schijfimage:</span><span class="sxs-lookup"><span data-stu-id="32077-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="32077-200">Nog steeds moet u opgeven of antwoord vraagt, alle extra parameters die zijn vereist voor de `azure vm create` opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="32077-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="32077-201">Meer informatie over de [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="32077-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="32077-202">Een virtuele machine met een JSON-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="32077-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="32077-203">Azure Resource Manager-sjablonen zijn JSON JavaScript Object Notation ()-bestanden waarmee de omgeving die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="32077-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="32077-204">De sjablonen zijn onderverdeeld andere resource providers zoals compute of een netwerk.</span><span class="sxs-lookup"><span data-stu-id="32077-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="32077-205">U kunt bestaande sjablonen gebruiken of uw eigen schrijven.</span><span class="sxs-lookup"><span data-stu-id="32077-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="32077-206">Lees meer over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32077-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="32077-207">Binnen de `Microsoft.Compute/virtualMachines` provider van de sjabloon die u hebt een `storageProfile` knooppunt dat de configuratiegegevens voor de virtuele machine bevat.</span><span class="sxs-lookup"><span data-stu-id="32077-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="32077-208">De twee belangrijkste parameters bewerken zijn de `image` en `vhd` URI's die verwijzen naar de installatiekopie van uw aangepaste schijf en de virtuele schijf van de nieuwe VM.</span><span class="sxs-lookup"><span data-stu-id="32077-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="32077-209">Hier volgt een voorbeeld van de JSON voor het gebruik van een aangepaste installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="32077-209">The following shows an example of the JSON for using a custom disk image:</span></span>

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

<span data-ttu-id="32077-210">U kunt [deze bestaande sjabloon te maken van een virtuele machine van een aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) of lezen over [maken van uw eigen Azure Resource Manager-sjablonen](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="32077-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="32077-211">Zodra u een sjabloon die is geconfigureerd hebt, hebt u uw virtuele machines met behulp van de `azure group deployment create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="32077-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="32077-212">Geef de URI van uw JSON-sjabloon met de `--template-uri` parameter:</span><span class="sxs-lookup"><span data-stu-id="32077-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="32077-213">Als u een JSON-bestand die lokaal zijn opgeslagen op uw computer hebt, kunt u de `--template-file` parameter in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="32077-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="32077-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32077-214">Next steps</span></span>
<span data-ttu-id="32077-215">Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32077-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="32077-216">U kunt ook [een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) naar uw nieuwe virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="32077-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="32077-217">Als u toepassingen die worden uitgevoerd op uw virtuele machines die u nodig hebt voor toegang tot hebt, moet u [openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32077-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

