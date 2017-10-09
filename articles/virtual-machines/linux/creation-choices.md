---
title: aaaDifferent manieren toocreate een Linux VM in Azure | Microsoft Azure
description: Meer informatie over Hallo verschillende manieren toocreate virtuele Linux-machine in Azure, met inbegrip van koppelingen tootools en zelfstudies voor elke methode.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="edb0c-103">Verschillende manieren toocreate een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="edb0c-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="edb0c-104">Hebt u Hallo flexibiliteit in Azure toocreate virtuele Linux-machine (VM) met behulp van hulpprogramma's en werkstromen vertrouwd tooyou.</span><span class="sxs-lookup"><span data-stu-id="edb0c-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="edb0c-105">In dit artikel bevat een overzicht van deze verschillen en voorbeelden voor het maken van uw virtuele Linux-machines, met inbegrip van hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="edb0c-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="edb0c-106">U kunt ook het maken van keuzen inclusief Hallo weergeven [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="edb0c-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="edb0c-107">Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) is beschikbaar in verschillende platforms via een pakket npm, geleverde distro pakketten of Docker-container.</span><span class="sxs-lookup"><span data-stu-id="edb0c-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="edb0c-108">Installeer de meest geschikte build Hallo voor uw omgeving en meld u aan tooan Azure-account met [az aanmelding](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="edb0c-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="edb0c-109">Maak een Linux-VM met hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="edb0c-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="edb0c-110">Maak een resourcegroep met [az group create](/cli/azure/group#create) met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="edb0c-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="edb0c-111">Maak een VM met [az vm maken](/cli/azure/vm#create) met de naam *myVM* met behulp van recente Hallo *UbuntuLTS* installatiekopie en SSH-sleutels genereren als deze niet al bestaan *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="edb0c-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="edb0c-112">Een virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="edb0c-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="edb0c-113">Hallo volgende voorbeeld wordt [az implementatie maken](/cli/azure/group/deployment#create) toocreate een virtuele machine uit een sjabloon die is opgeslagen op GitHub:</span><span class="sxs-lookup"><span data-stu-id="edb0c-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="edb0c-114">Een virtuele Linux-machine maken en aanpassen met cloud-init</span><span class="sxs-lookup"><span data-stu-id="edb0c-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="edb0c-115">Een maximaal beschikbare toepassing met gelijke taakverdeling maken op meerdere virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="edb0c-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="edb0c-116">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="edb0c-116">Azure portal</span></span>
<span data-ttu-id="edb0c-117">Hallo [Azure-portal](https://portal.azure.com) kunt u tooquickly een virtuele machine maken omdat er is niets tooinstall op uw systeem.</span><span class="sxs-lookup"><span data-stu-id="edb0c-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="edb0c-118">Gebruik hello Azure portal toocreate Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="edb0c-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="edb0c-119">Maak een Linux-VM met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="edb0c-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="edb0c-120">Opties voor besturingssysteem en installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="edb0c-120">Operating system and image choices</span></span>
<span data-ttu-id="edb0c-121">Wanneer u een virtuele machine maakt, kiest u een installatiekopie die op basis van het besturingssysteem die u wilt dat toorun Hallo.</span><span class="sxs-lookup"><span data-stu-id="edb0c-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="edb0c-122">Azure en de diverse partners bieden een groot aantal installatiekopieën. Sommige hiervan bevatten toepassingen en hulpprogramma’s die vooraf zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="edb0c-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="edb0c-123">Of een van uw eigen installatiekopieën uploaden (Zie [Hallo volgende sectie](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="edb0c-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="edb0c-124">Installatiekopieën van Azure</span><span class="sxs-lookup"><span data-stu-id="edb0c-124">Azure images</span></span>
<span data-ttu-id="edb0c-125">Gebruik Hallo [az vm-installatiekopie](/cli/azure/vm/image) toosee-opdrachten door de uitgever, distro release en builds beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="edb0c-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="edb0c-126">Beschikbare uitgevers vermelden:</span><span class="sxs-lookup"><span data-stu-id="edb0c-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="edb0c-127">Beschikbare producten (aanbiedingen) voor een bepaalde uitgever vermelden:</span><span class="sxs-lookup"><span data-stu-id="edb0c-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="edb0c-128">Beschikbare SKU's (distributiereleases) van een bepaalde aanbieding vermelden:</span><span class="sxs-lookup"><span data-stu-id="edb0c-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="edb0c-129">Alle beschikbare installatiekopieën voor een bepaalde release vermelden:</span><span class="sxs-lookup"><span data-stu-id="edb0c-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="edb0c-130">Zie voor meer voorbeelden op Bladeren en het gebruik van de beschikbare installatiekopieën [navigeren door en selecteren van installatiekopieën van virtuele machine van Azure met Azure CLI Hallo](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="edb0c-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="edb0c-131">Hallo [az vm maken](/cli/azure/vm#create) opdracht beschikt over aliassen kunt u tooquickly toegang Hallo veelvoorkomende distributies en hun meest recente versies.</span><span class="sxs-lookup"><span data-stu-id="edb0c-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="edb0c-132">Het gebruik van aliassen is vaak sneller dan het Hallo-uitgever, aanbieding, SKU en versie geven telkens wanneer die u een virtuele machine maken:</span><span class="sxs-lookup"><span data-stu-id="edb0c-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="edb0c-133">Alias</span><span class="sxs-lookup"><span data-stu-id="edb0c-133">Alias</span></span> | <span data-ttu-id="edb0c-134">Uitgever</span><span class="sxs-lookup"><span data-stu-id="edb0c-134">Publisher</span></span> | <span data-ttu-id="edb0c-135">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="edb0c-135">Offer</span></span> | <span data-ttu-id="edb0c-136">SKU</span><span class="sxs-lookup"><span data-stu-id="edb0c-136">SKU</span></span> | <span data-ttu-id="edb0c-137">Versie</span><span class="sxs-lookup"><span data-stu-id="edb0c-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="edb0c-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="edb0c-138">CentOS</span></span> |<span data-ttu-id="edb0c-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="edb0c-139">OpenLogic</span></span> |<span data-ttu-id="edb0c-140">Centos</span><span class="sxs-lookup"><span data-stu-id="edb0c-140">Centos</span></span> |<span data-ttu-id="edb0c-141">7.2</span><span class="sxs-lookup"><span data-stu-id="edb0c-141">7.2</span></span> |<span data-ttu-id="edb0c-142">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-142">latest</span></span> |
| <span data-ttu-id="edb0c-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="edb0c-143">CoreOS</span></span> |<span data-ttu-id="edb0c-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="edb0c-144">CoreOS</span></span> |<span data-ttu-id="edb0c-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="edb0c-145">CoreOS</span></span> |<span data-ttu-id="edb0c-146">Stabiel</span><span class="sxs-lookup"><span data-stu-id="edb0c-146">Stable</span></span> |<span data-ttu-id="edb0c-147">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-147">latest</span></span> |
| <span data-ttu-id="edb0c-148">Debian</span><span class="sxs-lookup"><span data-stu-id="edb0c-148">Debian</span></span> |<span data-ttu-id="edb0c-149">credativ</span><span class="sxs-lookup"><span data-stu-id="edb0c-149">credativ</span></span> |<span data-ttu-id="edb0c-150">Debian</span><span class="sxs-lookup"><span data-stu-id="edb0c-150">Debian</span></span> |<span data-ttu-id="edb0c-151">8</span><span class="sxs-lookup"><span data-stu-id="edb0c-151">8</span></span> |<span data-ttu-id="edb0c-152">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-152">latest</span></span> |
| <span data-ttu-id="edb0c-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="edb0c-153">openSUSE</span></span> |<span data-ttu-id="edb0c-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="edb0c-154">SUSE</span></span> |<span data-ttu-id="edb0c-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="edb0c-155">openSUSE</span></span> |<span data-ttu-id="edb0c-156">13.2</span><span class="sxs-lookup"><span data-stu-id="edb0c-156">13.2</span></span> |<span data-ttu-id="edb0c-157">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-157">latest</span></span> |
| <span data-ttu-id="edb0c-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="edb0c-158">RHEL</span></span> |<span data-ttu-id="edb0c-159">RedHat</span><span class="sxs-lookup"><span data-stu-id="edb0c-159">Redhat</span></span> |<span data-ttu-id="edb0c-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="edb0c-160">RHEL</span></span> |<span data-ttu-id="edb0c-161">7.2</span><span class="sxs-lookup"><span data-stu-id="edb0c-161">7.2</span></span> |<span data-ttu-id="edb0c-162">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-162">latest</span></span> |
| <span data-ttu-id="edb0c-163">SLES</span><span class="sxs-lookup"><span data-stu-id="edb0c-163">SLES</span></span> |<span data-ttu-id="edb0c-164">SLES</span><span class="sxs-lookup"><span data-stu-id="edb0c-164">SLES</span></span> |<span data-ttu-id="edb0c-165">SLES</span><span class="sxs-lookup"><span data-stu-id="edb0c-165">SLES</span></span> |<span data-ttu-id="edb0c-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="edb0c-166">12-SP1</span></span> |<span data-ttu-id="edb0c-167">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-167">latest</span></span> |
| <span data-ttu-id="edb0c-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="edb0c-168">UbuntuLTS</span></span> |<span data-ttu-id="edb0c-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="edb0c-169">Canonical</span></span> |<span data-ttu-id="edb0c-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="edb0c-170">UbuntuServer</span></span> |<span data-ttu-id="edb0c-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="edb0c-171">14.04.4-LTS</span></span> |<span data-ttu-id="edb0c-172">meest recente</span><span class="sxs-lookup"><span data-stu-id="edb0c-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="edb0c-173">Uw eigen installatiekopie gebruiken</span><span class="sxs-lookup"><span data-stu-id="edb0c-173">Use your own image</span></span>
<span data-ttu-id="edb0c-174">Als u specifieke aanpassingen nodig hebt, kunt u een installatiekopie gebruiken op basis van een bestaande VM in Azure door de betreffende VM vast te leggen.</span><span class="sxs-lookup"><span data-stu-id="edb0c-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="edb0c-175">U kunt ook een installatiekopie uploaden die u on-premises hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="edb0c-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="edb0c-176">Voor meer informatie over ondersteunde distributies en hoe toouse uw eigen installatiekopieën zien Hallo volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="edb0c-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="edb0c-177">Door Azure goedgekeurde distributies</span><span class="sxs-lookup"><span data-stu-id="edb0c-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="edb0c-178">Informatie over niet-goedgekeurde distributies</span><span class="sxs-lookup"><span data-stu-id="edb0c-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="edb0c-179">[Hoe een installatiekopie van een bestaande virtuele machine van Azure toocreate](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="edb0c-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="edb0c-180">Snel starten voorbeeld opdrachten toocreate een installatiekopie van een bestaande virtuele machine van Azure:</span><span class="sxs-lookup"><span data-stu-id="edb0c-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="edb0c-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edb0c-181">Next steps</span></span>
* <span data-ttu-id="edb0c-182">Maak een Linux-VM met Hallo [CLI](quick-create-cli.md), van Hallo [portal](quick-create-portal.md), of met behulp van een [Azure Resource Manager-sjabloon](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="edb0c-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="edb0c-183">Lees na het maken van een virtuele Linux-machine [meer informatie over Azure-schijven en opslag](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="edb0c-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="edb0c-184">Snelle stappen te[opnieuw instellen van een wachtwoord of SSH-sleutels en gebruikers beheren](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="edb0c-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
