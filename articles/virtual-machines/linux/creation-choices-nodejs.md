---
title: Verschillende manieren om te maken van een Linux-VM met Azure CLI 1.0 | Microsoft Docs
description: Informatie over de verschillende manieren om een virtuele Linux-machine te maken op Azure, waaronder koppelingen naar hulpprogramma's en zelfstudies voor elke methode.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="61f4d-103">Verschillende manieren om een virtuele Linux-machine te maken in Azure</span><span class="sxs-lookup"><span data-stu-id="61f4d-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="61f4d-104">In Azure hebt u de flexibiliteit om een virtuele Linux-machine te maken met behulp van hulpprogramma's en werkstromen die u prettig vindt.</span><span class="sxs-lookup"><span data-stu-id="61f4d-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="61f4d-105">Dit artikel bevat een overzicht van de verschillen en voorbeelden voor het maken van de Linux-VM's.</span><span class="sxs-lookup"><span data-stu-id="61f4d-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="61f4d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="61f4d-106">Azure CLI</span></span>
<span data-ttu-id="61f4d-107">Met een van de volgende CLI-versies kunt u virtuele machines maken in Azure:</span><span class="sxs-lookup"><span data-stu-id="61f4d-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="61f4d-108">Azure CLI 1.0: onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel (dit artikel)</span><span class="sxs-lookup"><span data-stu-id="61f4d-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="61f4d-109">[Azure CLI 2.0](../windows/creation-choices.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="61f4d-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="61f4d-110">De Azure CLI 1.0 is op diverse platforms beschikbaar via een npm-pakket, door distributeurs geleverde pakketten of Docker-container.</span><span class="sxs-lookup"><span data-stu-id="61f4d-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="61f4d-111">Meer informatie over het [installeren en configureren van de Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="61f4d-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="61f4d-112">In de volgende zelfstudies vindt u voorbeelden van het gebruik van de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="61f4d-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="61f4d-113">Lees elk artikel voor meer informatie over de vermelde Quick Start-opdrachten voor CLI:</span><span class="sxs-lookup"><span data-stu-id="61f4d-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="61f4d-114">Een virtuele Linux-machine maken via Azure CLI voor ontwikkeling en tests</span><span class="sxs-lookup"><span data-stu-id="61f4d-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="61f4d-115">Het volgende voorbeeld wordt een CoreOS VM die gebruikmaakt van een openbare sleutel met de naam *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="61f4d-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="61f4d-116">Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="61f4d-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="61f4d-117">In het volgende voorbeeld wordt een VM gemaakt met behulp van een op GitHub opgeslagen sjabloon:</span><span class="sxs-lookup"><span data-stu-id="61f4d-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="61f4d-118">Een volledige Linux-omgeving maken met de Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="61f4d-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="61f4d-119">Omvat het maken van een load balancer en meerdere VM’s in een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="61f4d-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="61f4d-120">Een schijf toevoegen aan een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="61f4d-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="61f4d-121">Het volgende voorbeeld wordt een *5* Gb schijf naar een bestaande virtuele machine met de naam *myVM*:</span><span class="sxs-lookup"><span data-stu-id="61f4d-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="61f4d-122">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61f4d-122">Azure portal</span></span>
<span data-ttu-id="61f4d-123">In [Azure Portal](https://portal.azure.com) kunt u snel een VM maken omdat u niets hoeft te installeren op uw systeem.</span><span class="sxs-lookup"><span data-stu-id="61f4d-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="61f4d-124">Azure Portal gebruiken om een virtuele machine te maken:</span><span class="sxs-lookup"><span data-stu-id="61f4d-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="61f4d-125">Een virtuele Linux-machine maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61f4d-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="61f4d-126">Opties voor besturingssysteem en installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="61f4d-126">Operating system and image choices</span></span>
<span data-ttu-id="61f4d-127">Bij het maken van een virtuele machine kiest u een installatiekopie op basis van het besturingssysteem dat u wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="61f4d-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="61f4d-128">Azure en de diverse partners bieden een groot aantal installatiekopieën. Sommige hiervan bevatten toepassingen en hulpprogramma’s die vooraf zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="61f4d-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="61f4d-129">U kunt ook een van uw eigen installatiekopieën uploaden (zie [het volgende gedeelte](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="61f4d-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="61f4d-130">Installatiekopieën van Azure</span><span class="sxs-lookup"><span data-stu-id="61f4d-130">Azure images</span></span>
<span data-ttu-id="61f4d-131">Gebruik de CLI-opdrachten van `azure vm image` om te zien wat er beschikbaar is per uitgever, distributierelease en build.</span><span class="sxs-lookup"><span data-stu-id="61f4d-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="61f4d-132">Vermeld beschikbare uitgevers als volgt:</span><span class="sxs-lookup"><span data-stu-id="61f4d-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="61f4d-133">Vermeld beschikbare producten (aanbiedingen) voor een bepaalde uitgever als volgt:</span><span class="sxs-lookup"><span data-stu-id="61f4d-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="61f4d-134">Vermeld beschikbare SKU's (distributiereleases) van een bepaalde aanbieding als volgt:</span><span class="sxs-lookup"><span data-stu-id="61f4d-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="61f4d-135">Vermeld alle beschikbare installatiekopieën voor een bepaalde release als volgt:</span><span class="sxs-lookup"><span data-stu-id="61f4d-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="61f4d-136">De opdrachten `azure vm quick-create` en `azure vm create` hebben aliassen waarmee u snel toegang kunt krijgen tot de meest voorkomende distributies en hun meest recente versies.</span><span class="sxs-lookup"><span data-stu-id="61f4d-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="61f4d-137">Het is gemakkelijker aliassen te gebruiken dan steeds weer de uitgever, aanbieding, SKU en versie op te geven wanneer u een VM maakt:</span><span class="sxs-lookup"><span data-stu-id="61f4d-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="61f4d-138">Alias</span><span class="sxs-lookup"><span data-stu-id="61f4d-138">Alias</span></span> | <span data-ttu-id="61f4d-139">Uitgever</span><span class="sxs-lookup"><span data-stu-id="61f4d-139">Publisher</span></span> | <span data-ttu-id="61f4d-140">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="61f4d-140">Offer</span></span> | <span data-ttu-id="61f4d-141">SKU</span><span class="sxs-lookup"><span data-stu-id="61f4d-141">SKU</span></span> | <span data-ttu-id="61f4d-142">Versie</span><span class="sxs-lookup"><span data-stu-id="61f4d-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="61f4d-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="61f4d-143">CentOS</span></span> |<span data-ttu-id="61f4d-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="61f4d-144">OpenLogic</span></span> |<span data-ttu-id="61f4d-145">Centos</span><span class="sxs-lookup"><span data-stu-id="61f4d-145">Centos</span></span> |<span data-ttu-id="61f4d-146">7.2</span><span class="sxs-lookup"><span data-stu-id="61f4d-146">7.2</span></span> |<span data-ttu-id="61f4d-147">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-147">latest</span></span> |
| <span data-ttu-id="61f4d-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="61f4d-148">CoreOS</span></span> |<span data-ttu-id="61f4d-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="61f4d-149">CoreOS</span></span> |<span data-ttu-id="61f4d-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="61f4d-150">CoreOS</span></span> |<span data-ttu-id="61f4d-151">Stabiel</span><span class="sxs-lookup"><span data-stu-id="61f4d-151">Stable</span></span> |<span data-ttu-id="61f4d-152">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-152">latest</span></span> |
| <span data-ttu-id="61f4d-153">Debian</span><span class="sxs-lookup"><span data-stu-id="61f4d-153">Debian</span></span> |<span data-ttu-id="61f4d-154">credativ</span><span class="sxs-lookup"><span data-stu-id="61f4d-154">credativ</span></span> |<span data-ttu-id="61f4d-155">Debian</span><span class="sxs-lookup"><span data-stu-id="61f4d-155">Debian</span></span> |<span data-ttu-id="61f4d-156">8</span><span class="sxs-lookup"><span data-stu-id="61f4d-156">8</span></span> |<span data-ttu-id="61f4d-157">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-157">latest</span></span> |
| <span data-ttu-id="61f4d-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="61f4d-158">openSUSE</span></span> |<span data-ttu-id="61f4d-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="61f4d-159">SUSE</span></span> |<span data-ttu-id="61f4d-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="61f4d-160">openSUSE</span></span> |<span data-ttu-id="61f4d-161">13.2</span><span class="sxs-lookup"><span data-stu-id="61f4d-161">13.2</span></span> |<span data-ttu-id="61f4d-162">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-162">latest</span></span> |
| <span data-ttu-id="61f4d-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="61f4d-163">RHEL</span></span> |<span data-ttu-id="61f4d-164">RedHat</span><span class="sxs-lookup"><span data-stu-id="61f4d-164">Redhat</span></span> |<span data-ttu-id="61f4d-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="61f4d-165">RHEL</span></span> |<span data-ttu-id="61f4d-166">7.2</span><span class="sxs-lookup"><span data-stu-id="61f4d-166">7.2</span></span> |<span data-ttu-id="61f4d-167">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-167">latest</span></span> |
| <span data-ttu-id="61f4d-168">SLES</span><span class="sxs-lookup"><span data-stu-id="61f4d-168">SLES</span></span> |<span data-ttu-id="61f4d-169">SLES</span><span class="sxs-lookup"><span data-stu-id="61f4d-169">SLES</span></span> |<span data-ttu-id="61f4d-170">SLES</span><span class="sxs-lookup"><span data-stu-id="61f4d-170">SLES</span></span> |<span data-ttu-id="61f4d-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="61f4d-171">12-SP1</span></span> |<span data-ttu-id="61f4d-172">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-172">latest</span></span> |
| <span data-ttu-id="61f4d-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="61f4d-173">UbuntuLTS</span></span> |<span data-ttu-id="61f4d-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="61f4d-174">Canonical</span></span> |<span data-ttu-id="61f4d-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="61f4d-175">UbuntuServer</span></span> |<span data-ttu-id="61f4d-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="61f4d-176">14.04.4-LTS</span></span> |<span data-ttu-id="61f4d-177">meest recente</span><span class="sxs-lookup"><span data-stu-id="61f4d-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="61f4d-178">Uw eigen installatiekopie gebruiken</span><span class="sxs-lookup"><span data-stu-id="61f4d-178">Use your own image</span></span>
<span data-ttu-id="61f4d-179">Als u specifieke aanpassingen nodig hebt, kunt u een installatiekopie gebruiken op basis van een bestaande VM in Azure door de betreffende VM *vast te leggen*.</span><span class="sxs-lookup"><span data-stu-id="61f4d-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="61f4d-180">U kunt ook een installatiekopie uploaden die u on-premises hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61f4d-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="61f4d-181">Raadpleeg de volgende artikelen voor meer informatie over ondersteunde distributies en over hoe u uw eigen installatiekopieën kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="61f4d-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="61f4d-182">Door Azure goedgekeurde distributies</span><span class="sxs-lookup"><span data-stu-id="61f4d-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="61f4d-183">Informatie over niet-goedgekeurde distributies</span><span class="sxs-lookup"><span data-stu-id="61f4d-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="61f4d-184">Een virtuele Linux-machine uploaden en maken op basis van een aangepaste installatiekopie</span><span class="sxs-lookup"><span data-stu-id="61f4d-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="61f4d-185">[Een virtuele Linux-machine vastleggen als Resource Manager-sjabloon](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="61f4d-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="61f4d-186">Voorbeelden van snelstartopdrachten voor het vastleggen van een bestaande VM:</span><span class="sxs-lookup"><span data-stu-id="61f4d-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="61f4d-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61f4d-187">Next steps</span></span>
* <span data-ttu-id="61f4d-188">Maak een virtuele Linux-machine via de [portal](quick-create-portal.md), met de [CLI](quick-create-cli.md) of met behulp van een Azure Resource Manager-[sjabloon](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="61f4d-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="61f4d-189">Nadat u een Linux-VM hebt gemaakt, [voegt u een gegevensschijf toe](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="61f4d-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="61f4d-190">Snelle stappen om [een wachtwoord of SSH-sleutels opnieuw in te stellen en gebruikers te beheren](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="61f4d-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

