---
title: aaaUpload of een kopie van een aangepaste Linux-VM met Azure CLI 2.0 | Microsoft Docs
description: "Upload of een aangepaste virtuele machine met behulp van Hallo Resource Manager-implementatiemodel en Azure CLI 2.0 Hallo kopiëren"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="cc013-103">Linux-VM te maken van aangepaste schijf Hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cc013-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="cc013-104">Dit artikel ziet u hoe tooupload een aangepaste virtuele harde schijf (VHD) of kopieer een een bestaande VHD in Azure en nieuwe virtuele Linux-machines (VM's) maken van aangepaste Hallo-schijf.</span><span class="sxs-lookup"><span data-stu-id="cc013-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="cc013-105">U kunt installeren en configureren van een Linux distro tooyour vereisten en gebruik vervolgens deze VHD tooquickly maakt een nieuwe virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="cc013-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="cc013-106">Als u wilt dat toocreate meerdere virtuele machines van de aangepaste schijf, maakt u een installatiekopie van een van de virtuele machine of de VHD.</span><span class="sxs-lookup"><span data-stu-id="cc013-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="cc013-107">Zie voor meer informatie [maken van een aangepaste installatiekopie van een virtuele machine van Azure CLI Hallo met](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="cc013-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="cc013-108">U hebt hiervoor twee opties:</span><span class="sxs-lookup"><span data-stu-id="cc013-108">You have two options:</span></span>
* [<span data-ttu-id="cc013-109">Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="cc013-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="cc013-110">Kopiëren van een bestaande virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="cc013-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="cc013-111">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="cc013-111">Quick commands</span></span>

<span data-ttu-id="cc013-112">Bij het maken van een nieuwe virtuele machine met [az vm maken](/cli/azure/vm#create) van een aangepaste of gespecialiseerde schijf u **koppelen** Hallo schijf (--koppelen-os-schijf) in plaats van een aangepaste of marketplace-installatiekopie (--afbeelding).</span><span class="sxs-lookup"><span data-stu-id="cc013-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="cc013-113">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* Hallo met beheerde-schijf met de naam *myManagedDisk* gemaakt op basis van uw aangepaste VHD:</span><span class="sxs-lookup"><span data-stu-id="cc013-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="cc013-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cc013-114">Requirements</span></span>
<span data-ttu-id="cc013-115">Hallo toocomplete volgende stappen die u nodig:</span><span class="sxs-lookup"><span data-stu-id="cc013-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="cc013-116">Een virtuele Linux-machine die is voorbereid voor gebruik in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc013-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="cc013-117">Hallo [voorbereiden Hallo VM](#prepare-the-vm) sectie van dit artikel bevat informatie over hoe toofind distro specifieke informatie over het installeren van Azure Linux Agent (waagent) is vereist voor Hallo VM toowork correct in Azure en u toobe kunnen tooconnect Hallo tooit via SSH.</span><span class="sxs-lookup"><span data-stu-id="cc013-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="cc013-118">Hallo VHD-bestand van een bestaand [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in VHD-indeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc013-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="cc013-119">Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:</span><span class="sxs-lookup"><span data-stu-id="cc013-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="cc013-120">Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling.</span><span class="sxs-lookup"><span data-stu-id="cc013-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="cc013-121">Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met **qemu img converteren**.</span><span class="sxs-lookup"><span data-stu-id="cc013-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="cc013-122">U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc013-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="cc013-123">Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc013-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="cc013-124">Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling.</span><span class="sxs-lookup"><span data-stu-id="cc013-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="cc013-125">Indien nodig, kunt u converteren VHDX schijven tooVHD [qemu img converteren](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cc013-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="cc013-126">Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="cc013-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="cc013-127">U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.</span><span class="sxs-lookup"><span data-stu-id="cc013-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="cc013-128">Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cc013-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="cc013-129">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="cc013-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="cc013-130">Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="cc013-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="cc013-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="cc013-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="cc013-132">Hallo VM voorbereiden</span><span class="sxs-lookup"><span data-stu-id="cc013-132">Prepare hello VM</span></span>

<span data-ttu-id="cc013-133">Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="cc013-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="cc013-134">Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund op Azure:</span><span class="sxs-lookup"><span data-stu-id="cc013-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="cc013-135">Op basis van centOS distributies</span><span class="sxs-lookup"><span data-stu-id="cc013-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cc013-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="cc013-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cc013-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="cc013-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cc013-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="cc013-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cc013-139">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="cc013-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cc013-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cc013-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="cc013-141">Andere - niet-goedgekeurde distributies</span><span class="sxs-lookup"><span data-stu-id="cc013-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="cc013-142">Zie ook Hallo [opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.</span><span class="sxs-lookup"><span data-stu-id="cc013-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="cc013-143">Hallo [Azure-platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) is van toepassing tooVMs met Linux alleen met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' wanneer een van de Hallo goedgekeurde distributies wordt gebruikt in [Linux op door Azure goedgekeurde Distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc013-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="cc013-144">Optie 1: Een VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="cc013-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="cc013-145">U kunt een aangepaste VHD die u hebt uitgevoerd op een lokale computer of die u hebt geëxporteerd uit een andere cloud uploaden.</span><span class="sxs-lookup"><span data-stu-id="cc013-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="cc013-146">toouse hello VHD toocreate een nieuwe virtuele machine in Azure, moet u tooupload Hallo VHD tooa storage-account en een beheerde schijf van Hallo VHD te maken.</span><span class="sxs-lookup"><span data-stu-id="cc013-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="cc013-147">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="cc013-147">Create a resource group</span></span>

<span data-ttu-id="cc013-148">Voordat het uploaden van uw aangepaste schijf en het maken van virtuele machines, moet u eerst toocreate een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cc013-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="cc013-149">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie: [overzicht van beheerde Azure-schijven](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cc013-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="cc013-150">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="cc013-150">Create a storage account</span></span>

<span data-ttu-id="cc013-151">Maken van een opslagaccount voor uw aangepaste schijf en virtuele machines met [az storage-account maken](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="cc013-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="cc013-152">Hallo volgende voorbeeld wordt een opslagaccount met de naam *mystorageaccount* in de resourcegroep Hallo eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cc013-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="cc013-153">Lijst met sleutels voor opslagaccount</span><span class="sxs-lookup"><span data-stu-id="cc013-153">List storage account keys</span></span>
<span data-ttu-id="cc013-154">Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert.</span><span class="sxs-lookup"><span data-stu-id="cc013-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="cc013-155">Deze toegangstoetsen worden gebruikt bij het verifiëren van toohello storage-account, zoals de uitvoering van schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="cc013-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="cc013-156">Lees meer over [het beheren van toegang tot toostorage hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cc013-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="cc013-157">U bekijkt hello toegangstoetsen met [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="cc013-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="cc013-158">Weergave Hallo toegangstoetsen voor Hallo storage-account die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cc013-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="cc013-159">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="cc013-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="cc013-160">Maak een notitie van **key1** terwijl u met deze toointeract met uw opslagaccount in de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc013-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="cc013-161">Een opslagcontainer maken</span><span class="sxs-lookup"><span data-stu-id="cc013-161">Create a storage container</span></span>
<span data-ttu-id="cc013-162">In Hallo dezelfde manier waarop u verschillende mappen toologically het lokale bestandssysteem organiseren, containers in een tooorganize storage-account maken van uw schijven.</span><span class="sxs-lookup"><span data-stu-id="cc013-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="cc013-163">Een opslagaccount kan een onbeperkt aantal containers bevatten.</span><span class="sxs-lookup"><span data-stu-id="cc013-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="cc013-164">Maken van een container met [az storage-container maken](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="cc013-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="cc013-165">Hallo volgende voorbeeld wordt een container met de naam *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="cc013-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="cc013-166">Hallo VHD uploaden</span><span class="sxs-lookup"><span data-stu-id="cc013-166">Upload hello VHD</span></span>
<span data-ttu-id="cc013-167">Nu uw aangepaste schijf met uploaden [uploaden van blob storage az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="cc013-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="cc013-168">U uploaden en de aangepaste schijf opslaan als een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="cc013-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="cc013-169">Geef uw toegangssleutel, Hallo-container die u hebt gemaakt in de vorige stap Hallo en vervolgens Hallo pad toohello aangepaste schijf op de lokale computer:</span><span class="sxs-lookup"><span data-stu-id="cc013-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="cc013-170">Bezig met uploaden Hallo VHD kan even duren.</span><span class="sxs-lookup"><span data-stu-id="cc013-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="cc013-171">Een beheerde schijf maken</span><span class="sxs-lookup"><span data-stu-id="cc013-171">Create a managed disk</span></span>


<span data-ttu-id="cc013-172">Maak een beheerde schijf vanuit Hallo VHD met [az schijf maken](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="cc013-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="cc013-173">Hallo volgende voorbeeld wordt een beheerde schijf met de naam *myManagedDisk* van Hallo VHD die u hebt geüpload tooyour opslagaccount en container met de naam:</span><span class="sxs-lookup"><span data-stu-id="cc013-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="cc013-174">Optie 2: Een bestaande virtuele machine kopiëren</span><span class="sxs-lookup"><span data-stu-id="cc013-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="cc013-175">U kunt ook maken Hallo aangepaste virtuele machine in Azure en vervolgens Hallo OS-schijf kopiëren en deze te koppelen tooa nieuwe VM toocreate een ander exemplaar.</span><span class="sxs-lookup"><span data-stu-id="cc013-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="cc013-176">Dit is goed voor het testen, maar als u toouse een bestaande virtuele machine van Azure als het Hallo-model voor meerdere nieuwe virtuele machines wilt, kunt u echt maken een **installatiekopie** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="cc013-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="cc013-177">Zie voor meer informatie over het maken van een installatiekopie van een bestaande virtuele machine van Azure [maken van een aangepaste installatiekopie van een virtuele machine in Azure met behulp van Hallo CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="cc013-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="cc013-178">Een momentopname maken</span><span class="sxs-lookup"><span data-stu-id="cc013-178">Create a snapshot</span></span>

<span data-ttu-id="cc013-179">In dit voorbeeld wordt een momentopname van een virtuele machine met de naam *myVM* in de resourcegroep *myResourceGroup* en maakt een momentopname met de naam *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="cc013-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="cc013-180">Hallo-beheerde schijven maken</span><span class="sxs-lookup"><span data-stu-id="cc013-180">Create hello managed disk</span></span>

<span data-ttu-id="cc013-181">Een nieuwe beheerde schijf van Hallo momentopname maken.</span><span class="sxs-lookup"><span data-stu-id="cc013-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="cc013-182">Hallo-ID van de momentopname Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="cc013-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="cc013-183">In dit voorbeeld Hallo momentopname heet *osDiskSnapshot* en is in Hallo *myResourceGroup* resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cc013-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="cc013-184">Hallo-beheerde schijven maken.</span><span class="sxs-lookup"><span data-stu-id="cc013-184">Create hello managed disk.</span></span> <span data-ttu-id="cc013-185">In dit voorbeeld wordt een beheerde schijf met de naam maakt *myManagedDisk* van onze momentopname die is 128 GB groot in standard-opslag.</span><span class="sxs-lookup"><span data-stu-id="cc013-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="cc013-186">Hallo VM maken</span><span class="sxs-lookup"><span data-stu-id="cc013-186">Create hello VM</span></span>

<span data-ttu-id="cc013-187">Maak nu uw virtuele machine met [az vm maken](/cli/azure/vm#create) en koppelt (--koppelen-os-schijf) Hallo beheerd schijf als Hallo OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="cc013-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="cc013-188">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myNewVM* Hallo met beheerde-schijf gemaakt op basis van uw geüploade VHD:</span><span class="sxs-lookup"><span data-stu-id="cc013-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="cc013-189">U moet kunnen tooSSH in Hallo VM met Hallo referenties van Hallo bron-VM.</span><span class="sxs-lookup"><span data-stu-id="cc013-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cc013-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc013-190">Next steps</span></span>
<span data-ttu-id="cc013-191">Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc013-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="cc013-192">U kunt ook te[een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nieuwe virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="cc013-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="cc013-193">Als u toepassingen die worden uitgevoerd op uw virtuele machines dat u tooaccess nodig hebt, moet u te[openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc013-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

