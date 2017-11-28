---
title: een aangepaste Linux-schijf met Azure CLI 2.0 aaaUpload | Microsoft Docs
description: Maken en uploaden van een virtuele harde schijf (VHD) tooAzure met Hallo Resource Manager-implementatiemodel en hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="7b3f3-103">Uploaden en Linux-VM te maken van aangepaste schijf Hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7b3f3-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="7b3f3-104">In dit artikel leest u hoe tooupload een virtuele harde schijf (VHD) tooan Azure storage-account met hello Azure CLI 2.0 en virtuele Linux-machines te maken van deze aangepaste schijf.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="7b3f3-105">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7b3f3-106">Deze functionaliteit kunt u tooinstall en configureren van een Linux distro tooyour vereisten en gebruik vervolgens deze VHD tooquickly Azure virtuele machines (VM's) maken.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="7b3f3-107">In dit onderwerp maakt gebruik van storage-accounts voor hello laatste VHD's, maar u kunt ook doen met behulp van deze stappen [schijven die worden beheerd](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="7b3f3-108">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="7b3f3-108">Quick commands</span></span>
<span data-ttu-id="7b3f3-109">Als u moet tooquickly Hallo taak, na de sectie details Hallo Hallo baseren opdrachten tooupload een tooAzure VHD.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="7b3f3-110">Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#requirements).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="7b3f3-111">Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="7b3f3-112">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7b3f3-113">Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="7b3f3-114">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7b3f3-115">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUs` locatie:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="7b3f3-116">Uw virtuele schijven met een toohold storage-account maken [az storage-account maken](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="7b3f3-117">Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="7b3f3-118">Hallo toegangssleutels voor uw opslagaccount met lijst [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="7b3f3-119">Maak een notitie van `key1`:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="7b3f3-120">Maken van een container in uw storage-account met behulp van de opslagsleutel Hallo u hebt verkregen met [az storage-container maken](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="7b3f3-121">Hallo volgende voorbeeld wordt een container met de naam `mydisks` met Hallo opslag sleutelwaarde van `key1`:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="7b3f3-122">Ten slotte uploaden uw VHD toohello-container die u hebt gemaakt met [uploaden van blob storage az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="7b3f3-123">Geef Hallo lokaal pad tooyour VHD onder `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="7b3f3-124">Geef Hallo URI tooyour schijf (`--image`) met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7b3f3-125">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` gebruik van de virtuele schijf Hallo eerder hebt geüpload:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="7b3f3-126">Hallo doelopslagaccount heeft toobe Hallo dezelfde als waar u de virtuele schijf geüpload.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="7b3f3-127">Of u kunt ook toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo **az vm maken** opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="7b3f3-128">U kunt meer lezen over Hallo [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="7b3f3-129">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b3f3-129">Requirements</span></span>
<span data-ttu-id="7b3f3-130">Hallo toocomplete volgende stappen die u nodig:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="7b3f3-131">**Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -installeren van een [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in VHD Hallo de indeling.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="7b3f3-132">Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="7b3f3-133">Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="7b3f3-134">Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="7b3f3-135">U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7b3f3-136">Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="7b3f3-137">Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="7b3f3-138">Indien nodig, kunt u converteren VHDX schijven tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="7b3f3-139">Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="7b3f3-140">U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="7b3f3-141">Virtuele machines die zijn gemaakt op basis van uw aangepaste schijf moeten zich bevinden in Hallo hetzelfde opslagaccount als Hallo schijf zelf</span><span class="sxs-lookup"><span data-stu-id="7b3f3-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="7b3f3-142">Maken van een storage-account en de container toohold uw aangepaste schijf en de gemaakte virtuele machines</span><span class="sxs-lookup"><span data-stu-id="7b3f3-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="7b3f3-143">Nadat u uw virtuele machines hebt gemaakt, kunt u veilig de schijf verwijderen</span><span class="sxs-lookup"><span data-stu-id="7b3f3-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="7b3f3-144">Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="7b3f3-145">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7b3f3-146">Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="7b3f3-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="7b3f3-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="7b3f3-148">Hallo schijf toobe geüpload voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7b3f3-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="7b3f3-149">Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="7b3f3-150">Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund op Azure:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="7b3f3-151">**[Op basis van centOS distributies](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7b3f3-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7b3f3-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7b3f3-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7b3f3-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7b3f3-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="7b3f3-157">**[Andere - niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="7b3f3-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="7b3f3-158">Zie ook Hallo  **[opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7b3f3-159">Hallo [Azure-platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) is van toepassing tooVMs met Linux alleen met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' wanneer een van de Hallo goedgekeurde distributies wordt gebruikt in [Linux op door Azure goedgekeurde Distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="7b3f3-160">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="7b3f3-160">Create a resource group</span></span>
<span data-ttu-id="7b3f3-161">Resourcegroepen samenbrengen logisch alle hello Azure-resources toosupport uw virtuele machines, zoals Hallo virtuele netwerken en opslag.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="7b3f3-162">Zie voor meer informatie resourcegroepen [resourcegroepen overzicht](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="7b3f3-163">Voordat het uploaden van uw aangepaste schijf en het maken van virtuele machines, moet u eerst toocreate een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="7b3f3-164">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="7b3f3-165">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="7b3f3-165">Create a storage account</span></span>

<span data-ttu-id="7b3f3-166">Maken van een opslagaccount voor uw aangepaste schijf en virtuele machines met [az storage-account maken](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="7b3f3-167">Geen VM's met niet-beheerde schijven die u maakt van uw aangepaste schijf nodig toobe in Hallo hetzelfde opslagaccount als die schijf.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="7b3f3-168">Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount` in de resourcegroep Hallo eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="7b3f3-169">Lijst met sleutels voor opslagaccount</span><span class="sxs-lookup"><span data-stu-id="7b3f3-169">List storage account keys</span></span>
<span data-ttu-id="7b3f3-170">Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="7b3f3-171">Deze toegangstoetsen worden gebruikt bij het verifiëren van toohello storage-account, zoals toocarry uit schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="7b3f3-172">Lees meer over [het beheren van toegang tot toostorage hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="7b3f3-173">U bekijkt hello toegangstoetsen met [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="7b3f3-174">Weergave Hallo toegangstoetsen voor Hallo storage-account die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="7b3f3-175">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="7b3f3-176">Maak een notitie van `key1` terwijl u met deze toointeract met uw opslagaccount in de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="7b3f3-177">Een opslagcontainer maken</span><span class="sxs-lookup"><span data-stu-id="7b3f3-177">Create a storage container</span></span>
<span data-ttu-id="7b3f3-178">In Hallo dezelfde manier waarop u verschillende mappen toologically het lokale bestandssysteem organiseren, containers in een tooorganize storage-account maken van uw schijven.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="7b3f3-179">Een opslagaccount kan een onbeperkt aantal containers bevatten.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="7b3f3-180">Maken van een container met [az storage-container maken](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="7b3f3-181">Hallo volgende voorbeeld wordt een container met de naam `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="7b3f3-182">Virtuele harde schijf geüpload</span><span class="sxs-lookup"><span data-stu-id="7b3f3-182">Upload VHD</span></span>
<span data-ttu-id="7b3f3-183">Nu uw aangepaste schijf met uploaden [uploaden van blob storage az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="7b3f3-184">U uploaden en de aangepaste schijf opslaan als een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="7b3f3-185">Geef uw toegangssleutel, Hallo-container die u hebt gemaakt in de vorige stap Hallo en vervolgens Hallo pad toohello aangepaste schijf op de lokale computer:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="7b3f3-186">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="7b3f3-186">Create hello VM</span></span>
<span data-ttu-id="7b3f3-187">een virtuele machine met niet-beheerde schijven toocreate Hallo URI tooyour schijf opgeven (`--image`) met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7b3f3-188">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` gebruik van de virtuele schijf Hallo eerder hebt geüpload:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="7b3f3-189">Geef van Hallo `--image` parameter met [az vm maken](/cli/azure/vm#create) toopoint tooyour aangepaste schijf.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="7b3f3-190">Zorg ervoor dat `--storage-account` komt overeen met Hallo opslagaccount waarin de aangepaste schijf wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="7b3f3-191">U beschikt niet over toouse Hallo dezelfde container als aangepaste schijf toostore Hallo uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="7b3f3-192">Zorg ervoor dat toocreate andere containers in Hallo dezelfde manier als Hallo eerdere stappen voordat u de aangepaste schijf uploadt.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="7b3f3-193">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` van uw aangepaste schijf:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="7b3f3-194">Of u kunt nog steeds toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo **az vm maken** opdracht zoals gebruikersnaam en het SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="7b3f3-195">Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="7b3f3-195">Resource Manager template</span></span>
<span data-ttu-id="7b3f3-196">Azure Resource Manager-sjablonen zijn JSON JavaScript Object Notation ()-bestanden die u wenst dat toobuild Hallo-omgeving definiëren.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="7b3f3-197">Hallo-sjablonen zijn onderverdeeld in de resourceproviders toodifferent zoals compute of een netwerk.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="7b3f3-198">U kunt bestaande sjablonen gebruiken of uw eigen schrijven.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="7b3f3-199">Lees meer over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="7b3f3-200">Binnen Hallo `Microsoft.Compute/virtualMachines` provider van de sjabloon die u hebt een `storageProfile` knooppunt met Hallo configuratiedetails voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="7b3f3-201">Hallo twee belangrijkste parameters tooedit zijn Hallo `image` en `vhd` URI's die verwijzen tooyour aangepaste en uw nieuwe VM virtuele schijf.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="7b3f3-202">Hallo hieronder toont een voorbeeld van Hallo JSON voor het gebruik van een aangepaste schijf:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="7b3f3-203">U kunt [deze bestaande sjabloon toocreate een virtuele machine van een aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) of lezen over [maken van uw eigen Azure Resource Manager-sjablonen](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="7b3f3-204">Zodra u een sjabloon die is geconfigureerd hebt, gebruikt u [az implementatie maken](/cli/azure/group/deployment#create) toocreate uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="7b3f3-205">Hallo-URI van de JSON-sjabloon opgeven met Hallo `--template-uri` parameter:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="7b3f3-206">Als u een JSON-bestand die lokaal zijn opgeslagen op uw computer hebt, kunt u Hallo `--template-file` parameter in plaats daarvan:</span><span class="sxs-lookup"><span data-stu-id="7b3f3-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="7b3f3-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b3f3-207">Next steps</span></span>
<span data-ttu-id="7b3f3-208">Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="7b3f3-209">U kunt ook te[een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nieuwe virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7b3f3-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="7b3f3-210">Als u toepassingen die worden uitgevoerd op uw virtuele machines dat u tooaccess nodig hebt, moet u te[openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b3f3-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

