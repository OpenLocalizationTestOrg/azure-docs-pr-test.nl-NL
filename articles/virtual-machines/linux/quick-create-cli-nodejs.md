---
title: Een virtuele Linux-machine maken met behulp van de Azure CLI 1.0 | Microsoft Docs
description: Een virtuele Linux-machine in Azure maken met de Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="6c498-103">Een virtuele Linux-machine maken met behulp van de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6c498-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="6c498-104">In dit artikel ziet u hoe u in Azure snel een virtuele Linux-machine (VM) kunt implementeren met behulp van de opdracht `azure vm quick-create` in de opdrachtregelinterface (CLI) van Azure.</span><span class="sxs-lookup"><span data-stu-id="6c498-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="6c498-105">Met de opdracht `quick-create` wordt een virtuele machine binnen een beveiligde basisinfrastructuur geïmplementeerd. Deze virtuele machine kunt u gebruiken als prototype of om snel een concept te testen.</span><span class="sxs-lookup"><span data-stu-id="6c498-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="6c498-106">Zie [Een virtuele machine maken met Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) als u een virtuele machine wilt maken met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="6c498-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6c498-107">U kunt een virtuele Linux-machine ook snel implementeren met behulp van de [Azure-portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c498-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6c498-108">In het artikel moet een [SSH openbare en persoonlijke sleutelbestanden](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c498-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="6c498-109">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="6c498-109">Quick commands</span></span>

<span data-ttu-id="6c498-110">In het volgende voorbeeld ziet u hoe u een virtuele CoreOS-machine implementeert en uw SSH-sleutel (Secure Shell) koppelt (uw argumenten kunnen afwijken):</span><span class="sxs-lookup"><span data-stu-id="6c498-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="6c498-111">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="6c498-111">Detailed walkthrough</span></span>

<span data-ttu-id="6c498-112">In het volgende overzicht wordt een virtuele UbuntuLTS-machine stapsgewijs geïmplementeerd, met uitleg over elke stap van de procedure.</span><span class="sxs-lookup"><span data-stu-id="6c498-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="6c498-113">Quick-create aliassen voor VM</span><span class="sxs-lookup"><span data-stu-id="6c498-113">VM quick-create aliases</span></span>

<span data-ttu-id="6c498-114">Als u snel een distributie wilt kiezen, kunt u de Azure CLI-aliassen gebruiken die aan de meest voorkomende OS-distributies zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6c498-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="6c498-115">De volgende tabel bevat de aliassen (vanaf Azure-CLI versie 0.10).</span><span class="sxs-lookup"><span data-stu-id="6c498-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="6c498-116">Alle implementaties die gebruikmaken van `quick-create` zijn standaard virtuele machines die worden ondersteund door SSD-opslag (Solid-State Drive). Dit staat garant voor snelle inrichting en snelle toegang tot de schijf.</span><span class="sxs-lookup"><span data-stu-id="6c498-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="6c498-117">(Deze aliassen vertegenwoordigen een klein gedeelte van de beschikbare distributies in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c498-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="6c498-118">Meer installatiekopieën vindt u in de Azure Marketplace door te [zoeken naar een installatiekopie in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [op het web](https://azure.microsoft.com/marketplace/virtual-machines/) maar u kunt ook [uw eigen aangepaste installatiekopie uploaden](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="6c498-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="6c498-119">Alias</span><span class="sxs-lookup"><span data-stu-id="6c498-119">Alias</span></span> | <span data-ttu-id="6c498-120">Uitgever</span><span class="sxs-lookup"><span data-stu-id="6c498-120">Publisher</span></span> | <span data-ttu-id="6c498-121">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="6c498-121">Offer</span></span> | <span data-ttu-id="6c498-122">SKU</span><span class="sxs-lookup"><span data-stu-id="6c498-122">SKU</span></span> | <span data-ttu-id="6c498-123">Versie</span><span class="sxs-lookup"><span data-stu-id="6c498-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="6c498-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="6c498-124">CentOS</span></span> |<span data-ttu-id="6c498-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6c498-125">OpenLogic</span></span> |<span data-ttu-id="6c498-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="6c498-126">CentOS</span></span> |<span data-ttu-id="6c498-127">7.2</span><span class="sxs-lookup"><span data-stu-id="6c498-127">7.2</span></span> |<span data-ttu-id="6c498-128">meest recente</span><span class="sxs-lookup"><span data-stu-id="6c498-128">latest</span></span> |
| <span data-ttu-id="6c498-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6c498-129">CoreOS</span></span> |<span data-ttu-id="6c498-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6c498-130">CoreOS</span></span> |<span data-ttu-id="6c498-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6c498-131">CoreOS</span></span> |<span data-ttu-id="6c498-132">Stabiel</span><span class="sxs-lookup"><span data-stu-id="6c498-132">Stable</span></span> |<span data-ttu-id="6c498-133">meest recente</span><span class="sxs-lookup"><span data-stu-id="6c498-133">latest</span></span> |
| <span data-ttu-id="6c498-134">Debian</span><span class="sxs-lookup"><span data-stu-id="6c498-134">Debian</span></span> |<span data-ttu-id="6c498-135">credativ</span><span class="sxs-lookup"><span data-stu-id="6c498-135">credativ</span></span> |<span data-ttu-id="6c498-136">Debian</span><span class="sxs-lookup"><span data-stu-id="6c498-136">Debian</span></span> |<span data-ttu-id="6c498-137">8</span><span class="sxs-lookup"><span data-stu-id="6c498-137">8</span></span> |<span data-ttu-id="6c498-138">meest recente</span><span class="sxs-lookup"><span data-stu-id="6c498-138">latest</span></span> |
| <span data-ttu-id="6c498-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6c498-139">openSUSE</span></span> |<span data-ttu-id="6c498-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="6c498-140">SUSE</span></span> |<span data-ttu-id="6c498-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6c498-141">openSUSE</span></span> |<span data-ttu-id="6c498-142">13.2</span><span class="sxs-lookup"><span data-stu-id="6c498-142">13.2</span></span> |<span data-ttu-id="6c498-143">meest recente</span><span class="sxs-lookup"><span data-stu-id="6c498-143">latest</span></span> |
| <span data-ttu-id="6c498-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="6c498-144">RHEL</span></span> |<span data-ttu-id="6c498-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="6c498-145">Red Hat</span></span> |<span data-ttu-id="6c498-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="6c498-146">RHEL</span></span> |<span data-ttu-id="6c498-147">7.2</span><span class="sxs-lookup"><span data-stu-id="6c498-147">7.2</span></span> |<span data-ttu-id="6c498-148">meest recente</span><span class="sxs-lookup"><span data-stu-id="6c498-148">latest</span></span> |
| <span data-ttu-id="6c498-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="6c498-149">UbuntuLTS</span></span> |<span data-ttu-id="6c498-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="6c498-150">Canonical</span></span> |<span data-ttu-id="6c498-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="6c498-151">Ubuntu Server</span></span> |<span data-ttu-id="6c498-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="6c498-152">14.04.4-LTS</span></span> |<span data-ttu-id="6c498-153">meest recente</span><span class="sxs-lookup"><span data-stu-id="6c498-153">latest</span></span> |

<span data-ttu-id="6c498-154">In de volgende secties wordt de `UbuntuLTS`-alias voor de optie **ImageURN** gebruikt (`-Q`) om een Ubuntu 14.04.4 LTS Server te implementeren.</span><span class="sxs-lookup"><span data-stu-id="6c498-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="6c498-155">In het vorige voorbeeld van `quick-create` wordt alleen de vlag `-M` gebruikt om de openbare SSH-sleutel te identificeren die moet worden geüpload. Ondertussen worden SSH-wachtwoorden uitgeschakeld. U wordt daarom gevraagd naar de volgende argumenten:</span><span class="sxs-lookup"><span data-stu-id="6c498-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="6c498-156">de naam van de resourcegroep (voor een eerste Azure-resourcegroep is doorgaans elke willekeurige tekenreeks geschikt )</span><span class="sxs-lookup"><span data-stu-id="6c498-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="6c498-157">VM-naam</span><span class="sxs-lookup"><span data-stu-id="6c498-157">VM name</span></span>
* <span data-ttu-id="6c498-158">locatie (`westus` of `westeurope` zijn goede standaardwaarden)</span><span class="sxs-lookup"><span data-stu-id="6c498-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="6c498-159">Linux (om in Azure aan te geven welk besturingssysteem u wilt)</span><span class="sxs-lookup"><span data-stu-id="6c498-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="6c498-160">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="6c498-160">username</span></span>

<span data-ttu-id="6c498-161">In het volgende voorbeeld worden alle waarden opgegeven, zodat er geen verdere vragen worden gesteld.</span><span class="sxs-lookup"><span data-stu-id="6c498-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="6c498-162">Als u een `~/.ssh/id_rsa.pub` als openbaar-sleutelbestand met ssh-rsa-indeling hebt, werkt alles:</span><span class="sxs-lookup"><span data-stu-id="6c498-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="6c498-163">Uw uitvoer moet eruitzien als in het volgende uitvoerblok:</span><span class="sxs-lookup"><span data-stu-id="6c498-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="6c498-164">Aanmelden bij de nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6c498-164">Log in to the new VM</span></span>
<span data-ttu-id="6c498-165">Meld u met het openbare IP-adres dat in de uitvoer staat vermeld aan bij uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6c498-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="6c498-166">U kunt ook de volledig gekwalificeerde domeinnaam (FQDN) gebruiken die wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="6c498-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="6c498-167">De aanmeldingsprocedure moet er ongeveer als het volgende uitvoerblok uitzien:</span><span class="sxs-lookup"><span data-stu-id="6c498-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="6c498-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c498-168">Next steps</span></span>
<span data-ttu-id="6c498-169">De opdracht `azure vm quick-create` is een goede manier om snel een virtuele machine te implementeren, zodat u zich kunt aanmelden bij een bash-shell en aan de slag kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="6c498-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="6c498-170">Wanneer u `vm quick-create` gebruikt, hebt u echter geen uitgebreide controle en kunt u geen complexere omgeving maken.</span><span class="sxs-lookup"><span data-stu-id="6c498-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="6c498-171">Als u een virtuele Linux-machine wilt implementeren die is afgestemd op uw infrastructuur, volg dan de instructies in een van deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="6c498-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="6c498-172">Rechtstreeks uw eigen aangepaste omgeving maken voor een virtuele Linux-machine met Azure CLI-opdrachten</span><span class="sxs-lookup"><span data-stu-id="6c498-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6c498-173">Een met SSH beveiligde virtuele Linux-machine in Azure maken met behulp van sjablonen</span><span class="sxs-lookup"><span data-stu-id="6c498-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="6c498-174">U kunt ook [het Azure-stuurprogramma `docker-machine` gebruiken dat verschillende opdrachten heeft om snel een Linux-VM als een docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) te maken.</span><span class="sxs-lookup"><span data-stu-id="6c498-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
