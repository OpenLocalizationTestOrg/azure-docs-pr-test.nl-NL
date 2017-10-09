---
title: aaaUsing cloud init toocustomize een Linux-VM tijdens het maken in Azure | Microsoft Docs
description: Hoe toouse cloud init toocustomize een Linux-VM tijdens het maken met Azure CLI 1.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="99db7-103">Cloud-init toocustomize een Linux-VM te gebruiken tijdens het maken van Hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="99db7-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="99db7-104">Dit artikel laat zien hoe toomake een cloud-init script tooset Hallo hostnaam, geïnstalleerde pakketten bijwerken en beheren van gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="99db7-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="99db7-105">Hallo cloud init scripts worden aangeroepen tijdens Hallo maken van virtuele machines van Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="99db7-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="99db7-106">Hallo artikel is vereist:</span><span class="sxs-lookup"><span data-stu-id="99db7-106">hello article requires:</span></span>

* <span data-ttu-id="99db7-107">een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="99db7-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="99db7-108">Hallo [Azure CLI](../../cli-install-nodejs.md) aangemeld `azure login`.</span><span class="sxs-lookup"><span data-stu-id="99db7-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="99db7-109">Hello Azure CLI *moet* modus Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="99db7-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="99db7-110">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="99db7-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="99db7-111">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="99db7-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="99db7-112">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="99db7-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="99db7-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="99db7-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="99db7-114">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="99db7-114">Quick Commands</span></span>
<span data-ttu-id="99db7-115">Maak een cloud-init.txt-script waarmee Hallo-hostnaam ingesteld, werkt u alle pakketten en voegt een gebruiker sudo tooLinux.</span><span class="sxs-lookup"><span data-stu-id="99db7-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
<span data-ttu-id="99db7-116">Maak een groep resource toolaunch virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="99db7-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="99db7-117">Maak een Linux-VM met behulp van cloud-init tooconfigure deze tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="99db7-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="99db7-118">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="99db7-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="99db7-119">Inleiding</span><span class="sxs-lookup"><span data-stu-id="99db7-119">Introduction</span></span>
<span data-ttu-id="99db7-120">Wanneer u een nieuwe Linux VM start, kunt u een standaard Linux-VM met niets wel aangepaste of gereed voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="99db7-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="99db7-121">[Cloud-init](https://cloudinit.readthedocs.org) is een normale manier tooinject als deze wordt opgestart voor Hallo waarvoor de eerste keer een script of configuratie-instellingen in die Linux VM.</span><span class="sxs-lookup"><span data-stu-id="99db7-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="99db7-122">In Azure, er zijn drie manieren toomake wijzigingen naar een Linux-VM als dit wordt geïmplementeerd of opgestart.</span><span class="sxs-lookup"><span data-stu-id="99db7-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="99db7-123">Scripts met cloud-init invoeren.</span><span class="sxs-lookup"><span data-stu-id="99db7-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="99db7-124">Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99db7-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="99db7-125">Een Azure-sjabloon met behulp van cloud-init.</span><span class="sxs-lookup"><span data-stu-id="99db7-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="99db7-126">Een Azure-sjabloon met [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99db7-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="99db7-127">tooinject scripts op elk gewenst moment na opstarten:</span><span class="sxs-lookup"><span data-stu-id="99db7-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="99db7-128">SSH toorun opdrachten rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="99db7-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="99db7-129">Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively of in een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="99db7-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="99db7-130">Configuration management-hulpprogramma's zoals Ansible, Salt of Chef of Puppet.</span><span class="sxs-lookup"><span data-stu-id="99db7-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="99db7-131">: VMAccess-extensie wordt uitgevoerd voor een script zoals root in Hallo dezelfde manier via SSH kunt.</span><span class="sxs-lookup"><span data-stu-id="99db7-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="99db7-132">Echter kan met behulp van de VM-extensie Hallo verschillende functies die Azure biedt die nuttig is afhankelijk van uw scenario kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="99db7-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="99db7-133">Cloud-init beschikbaarheid op Azure VM snelle invoer installatiekopie aliassen:</span><span class="sxs-lookup"><span data-stu-id="99db7-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="99db7-134">Alias</span><span class="sxs-lookup"><span data-stu-id="99db7-134">Alias</span></span> | <span data-ttu-id="99db7-135">Uitgever</span><span class="sxs-lookup"><span data-stu-id="99db7-135">Publisher</span></span> | <span data-ttu-id="99db7-136">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="99db7-136">Offer</span></span> | <span data-ttu-id="99db7-137">SKU</span><span class="sxs-lookup"><span data-stu-id="99db7-137">SKU</span></span> | <span data-ttu-id="99db7-138">Versie</span><span class="sxs-lookup"><span data-stu-id="99db7-138">Version</span></span> | <span data-ttu-id="99db7-139">cloud-init</span><span class="sxs-lookup"><span data-stu-id="99db7-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="99db7-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="99db7-140">CentOS</span></span> |<span data-ttu-id="99db7-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="99db7-141">OpenLogic</span></span> |<span data-ttu-id="99db7-142">Centos</span><span class="sxs-lookup"><span data-stu-id="99db7-142">Centos</span></span> |<span data-ttu-id="99db7-143">7.2</span><span class="sxs-lookup"><span data-stu-id="99db7-143">7.2</span></span> |<span data-ttu-id="99db7-144">meest recente</span><span class="sxs-lookup"><span data-stu-id="99db7-144">latest</span></span> |<span data-ttu-id="99db7-145">Er is geen</span><span class="sxs-lookup"><span data-stu-id="99db7-145">no</span></span> |
| <span data-ttu-id="99db7-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="99db7-146">CoreOS</span></span> |<span data-ttu-id="99db7-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="99db7-147">CoreOS</span></span> |<span data-ttu-id="99db7-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="99db7-148">CoreOS</span></span> |<span data-ttu-id="99db7-149">Stabiel</span><span class="sxs-lookup"><span data-stu-id="99db7-149">Stable</span></span> |<span data-ttu-id="99db7-150">meest recente</span><span class="sxs-lookup"><span data-stu-id="99db7-150">latest</span></span> |<span data-ttu-id="99db7-151">Ja</span><span class="sxs-lookup"><span data-stu-id="99db7-151">yes</span></span> |
| <span data-ttu-id="99db7-152">Debian</span><span class="sxs-lookup"><span data-stu-id="99db7-152">Debian</span></span> |<span data-ttu-id="99db7-153">credativ</span><span class="sxs-lookup"><span data-stu-id="99db7-153">credativ</span></span> |<span data-ttu-id="99db7-154">Debian</span><span class="sxs-lookup"><span data-stu-id="99db7-154">Debian</span></span> |<span data-ttu-id="99db7-155">8</span><span class="sxs-lookup"><span data-stu-id="99db7-155">8</span></span> |<span data-ttu-id="99db7-156">meest recente</span><span class="sxs-lookup"><span data-stu-id="99db7-156">latest</span></span> |<span data-ttu-id="99db7-157">Er is geen</span><span class="sxs-lookup"><span data-stu-id="99db7-157">no</span></span> |
| <span data-ttu-id="99db7-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="99db7-158">openSUSE</span></span> |<span data-ttu-id="99db7-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="99db7-159">SUSE</span></span> |<span data-ttu-id="99db7-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="99db7-160">openSUSE</span></span> |<span data-ttu-id="99db7-161">13.2</span><span class="sxs-lookup"><span data-stu-id="99db7-161">13.2</span></span> |<span data-ttu-id="99db7-162">meest recente</span><span class="sxs-lookup"><span data-stu-id="99db7-162">latest</span></span> |<span data-ttu-id="99db7-163">Er is geen</span><span class="sxs-lookup"><span data-stu-id="99db7-163">no</span></span> |
| <span data-ttu-id="99db7-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="99db7-164">RHEL</span></span> |<span data-ttu-id="99db7-165">RedHat</span><span class="sxs-lookup"><span data-stu-id="99db7-165">Redhat</span></span> |<span data-ttu-id="99db7-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="99db7-166">RHEL</span></span> |<span data-ttu-id="99db7-167">7.2</span><span class="sxs-lookup"><span data-stu-id="99db7-167">7.2</span></span> |<span data-ttu-id="99db7-168">meest recente</span><span class="sxs-lookup"><span data-stu-id="99db7-168">latest</span></span> |<span data-ttu-id="99db7-169">Er is geen</span><span class="sxs-lookup"><span data-stu-id="99db7-169">no</span></span> |
| <span data-ttu-id="99db7-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="99db7-170">UbuntuLTS</span></span> |<span data-ttu-id="99db7-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="99db7-171">Canonical</span></span> |<span data-ttu-id="99db7-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="99db7-172">UbuntuServer</span></span> |<span data-ttu-id="99db7-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="99db7-173">14.04.4-LTS</span></span> |<span data-ttu-id="99db7-174">meest recente</span><span class="sxs-lookup"><span data-stu-id="99db7-174">latest</span></span> |<span data-ttu-id="99db7-175">Ja</span><span class="sxs-lookup"><span data-stu-id="99db7-175">yes</span></span> |

<span data-ttu-id="99db7-176">Microsoft is werken met onze partners tooget cloud-init opgenomen en werken in dat ze tooAzure bieden Hallo-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="99db7-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="99db7-177">Toevoegen van een cloud-init script toohello maken van VM's met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="99db7-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="99db7-178">toolaunch een cloud-init-script bij het maken van een virtuele machine in Azure, geef Hallo cloud init-bestand met hello Azure CLI `--custom-data` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="99db7-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="99db7-179">Maak een groep resource toolaunch virtuele machines in.</span><span class="sxs-lookup"><span data-stu-id="99db7-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="99db7-180">Maak een Linux-VM met behulp van cloud-init tooconfigure deze tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="99db7-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="99db7-181">Maken van een cloud-init script tooset Hallo hostnaam van een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="99db7-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="99db7-182">Een van de belangrijkste instellingen voor een Linux-VM en eenvoudigste Hallo zijn Hallo hostnaam.</span><span class="sxs-lookup"><span data-stu-id="99db7-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="99db7-183">We kunnen eenvoudig Stel dit met behulp van cloud-init met dit script.</span><span class="sxs-lookup"><span data-stu-id="99db7-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="99db7-184">Voorbeeld van de cloud init script met de naam `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="99db7-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="99db7-185">Tijdens opstarten Hallo Hallo VM stelt dit script cloud init Hallo hostnaam te`myservername`.</span><span class="sxs-lookup"><span data-stu-id="99db7-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="99db7-186">Aanmelding en controleer of de hostnaam Hallo Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="99db7-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="99db7-187">Een cloud-init script tooupdate Linux maken</span><span class="sxs-lookup"><span data-stu-id="99db7-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="99db7-188">Voor beveiliging moet uw tooupdate Ubuntu VM op Hallo eerst wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="99db7-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="99db7-189">Met behulp van cloud-init kunt we doen dat script, afhankelijk van de Linux-distributie Hallo u Hello volgen.</span><span class="sxs-lookup"><span data-stu-id="99db7-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="99db7-190">Cloud-init voorbeeldscript `cloud_config_apt_upgrade.txt` voor Hallo Debian-familie</span><span class="sxs-lookup"><span data-stu-id="99db7-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="99db7-191">Nadat Linux is opgestart, alle geïnstalleerd hello-pakketten worden bijgewerkt via `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="99db7-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="99db7-192">Aanmelding en controleer of alle pakketten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="99db7-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="99db7-193">Maken van een script cloud init tooadd een tooLinux gebruiker</span><span class="sxs-lookup"><span data-stu-id="99db7-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="99db7-194">Een Hallo eerste taken op een nieuwe Linux-VM is een gebruiker voor uzelf of met behulp van tooavoid tooadd `root`.</span><span class="sxs-lookup"><span data-stu-id="99db7-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="99db7-195">SSH-sleutels zijn best practice voor beveiliging en bruikbaarheid en ze worden toegevoegd toohello `~/.ssh/authorized_keys` bestand met dit script cloud init.</span><span class="sxs-lookup"><span data-stu-id="99db7-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="99db7-196">Cloud-init voorbeeldscript `cloud_config_add_users.txt` voor Debian-familie</span><span class="sxs-lookup"><span data-stu-id="99db7-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="99db7-197">Nadat Linux is opgestart, zijn alle gebruikers van de vermelde Hallo gemaakt en toegevoegd toohello sudo-groep.</span><span class="sxs-lookup"><span data-stu-id="99db7-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="99db7-198">Aanmelding en verificatie van gebruiker Hallo nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99db7-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="99db7-199">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="99db7-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="99db7-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99db7-200">Next Steps</span></span>
<span data-ttu-id="99db7-201">Cloud-init wordt steeds een standaardmanier toomodify uw Linux VM op opstarten.</span><span class="sxs-lookup"><span data-stu-id="99db7-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="99db7-202">Azure heeft bovendien VM-extensies u toomodify kunnen uw LinuxVM op opstarten of terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99db7-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="99db7-203">U kunt bijvoorbeeld gebruikersgegevens of hello Azure VMAccessExtension tooreset SSH gebruiken terwijl Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99db7-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="99db7-204">Met cloud-init moet u een wachtwoord opnieuw opstarten tooreset Hallo.</span><span class="sxs-lookup"><span data-stu-id="99db7-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="99db7-205">Over functies en uitbreidingen van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="99db7-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="99db7-206">Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="99db7-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

