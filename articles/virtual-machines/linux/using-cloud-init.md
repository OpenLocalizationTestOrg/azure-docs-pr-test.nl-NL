---
title: aaaUse cloud init toocustomize een Linux-VM | Microsoft Docs
description: Hoe toouse cloud init toocustomize een Linux-VM tijdens het maken met Azure CLI 2.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="ebd81-103">Cloud-init toocustomize een Linux-VM te gebruiken tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="ebd81-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="ebd81-104">In dit artikel leest u hoe toomake een cloud-init script tooset Hallo hostnaam, geïnstalleerde pakketten bijwerken en beheren van gebruikersaccounts Hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ebd81-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="ebd81-105">Hallo cloud init scripts worden aangeroepen wanneer u een virtuele machine (VM) van Azure CLI maken.</span><span class="sxs-lookup"><span data-stu-id="ebd81-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="ebd81-106">Zie voor een meer gedetailleerd overzicht over het installeren van toepassingen, configuratiebestanden schrijven en injecteren sleutels van de Sleutelkluis, [in deze zelfstudie](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ebd81-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="ebd81-107">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ebd81-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ebd81-108">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="ebd81-108">Quick commands</span></span>
<span data-ttu-id="ebd81-109">Maak een cloud-init.txt-script waarmee Hallo-hostnaam ingesteld, werkt u alle pakketten en voegt een gebruiker sudo tooLinux.</span><span class="sxs-lookup"><span data-stu-id="ebd81-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```yaml
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

<span data-ttu-id="ebd81-110">Maken van een groep resource toolaunch virtuele machines in met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ebd81-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ebd81-111">Hallo volgende voorbeeld maakt Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ebd81-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ebd81-112">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) cloud init tooconfigure met deze tijdens het opstarten Hello `--custom-data` parameter.</span><span class="sxs-lookup"><span data-stu-id="ebd81-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ebd81-113">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="ebd81-113">Detailed walkthrough</span></span>
<span data-ttu-id="ebd81-114">Wanneer u een nieuwe Linux VM start, kunt u een standaard Linux-VM met niets wel aangepaste of gereed voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="ebd81-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="ebd81-115">[Cloud-init](https://cloudinit.readthedocs.org) is een normale manier tooinject als deze wordt opgestart voor Hallo waarvoor de eerste keer een script of configuratie-instellingen in die Linux VM.</span><span class="sxs-lookup"><span data-stu-id="ebd81-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="ebd81-116">In Azure, er zijn diverse manieren toomake wijzigingen naar een Linux-VM als dit wordt geïmplementeerd of opgestart.</span><span class="sxs-lookup"><span data-stu-id="ebd81-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="ebd81-117">Scripts met cloud-init invoeren.</span><span class="sxs-lookup"><span data-stu-id="ebd81-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="ebd81-118">Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ebd81-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="ebd81-119">Een Azure-sjabloon met behulp van cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ebd81-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="ebd81-120">Een Azure-sjabloon met [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="ebd81-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="ebd81-121">tooinject scripts op elk gewenst moment na opstarten:</span><span class="sxs-lookup"><span data-stu-id="ebd81-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="ebd81-122">SSH toorun opdrachten rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="ebd81-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="ebd81-123">Scripts met hello Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md), imperatively of in een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="ebd81-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="ebd81-124">Configuration management-hulpprogramma's zoals Ansible, Salt of Chef of Puppet.</span><span class="sxs-lookup"><span data-stu-id="ebd81-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="ebd81-125">VMAccess-extensie wordt uitgevoerd voor een script zoals root in Hallo dezelfde manier via SSH kunt.</span><span class="sxs-lookup"><span data-stu-id="ebd81-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="ebd81-126">Echter kan met behulp van de VM-extensie Hallo verschillende functies die Azure biedt die nuttig is afhankelijk van uw scenario kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="ebd81-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="ebd81-127">Cloud-init beschikbaarheid op Azure VM snelle invoer installatiekopie aliassen:</span><span class="sxs-lookup"><span data-stu-id="ebd81-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="ebd81-128">Alias</span><span class="sxs-lookup"><span data-stu-id="ebd81-128">Alias</span></span> | <span data-ttu-id="ebd81-129">Uitgever</span><span class="sxs-lookup"><span data-stu-id="ebd81-129">Publisher</span></span> | <span data-ttu-id="ebd81-130">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="ebd81-130">Offer</span></span> | <span data-ttu-id="ebd81-131">SKU</span><span class="sxs-lookup"><span data-stu-id="ebd81-131">SKU</span></span> | <span data-ttu-id="ebd81-132">Versie</span><span class="sxs-lookup"><span data-stu-id="ebd81-132">Version</span></span> | <span data-ttu-id="ebd81-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="ebd81-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="ebd81-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="ebd81-134">CentOS</span></span> |<span data-ttu-id="ebd81-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="ebd81-135">OpenLogic</span></span> |<span data-ttu-id="ebd81-136">Centos</span><span class="sxs-lookup"><span data-stu-id="ebd81-136">Centos</span></span> |<span data-ttu-id="ebd81-137">7.2</span><span class="sxs-lookup"><span data-stu-id="ebd81-137">7.2</span></span> |<span data-ttu-id="ebd81-138">meest recente</span><span class="sxs-lookup"><span data-stu-id="ebd81-138">latest</span></span> |<span data-ttu-id="ebd81-139">Er is geen</span><span class="sxs-lookup"><span data-stu-id="ebd81-139">no</span></span> |
| <span data-ttu-id="ebd81-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ebd81-140">CoreOS</span></span> |<span data-ttu-id="ebd81-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ebd81-141">CoreOS</span></span> |<span data-ttu-id="ebd81-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ebd81-142">CoreOS</span></span> |<span data-ttu-id="ebd81-143">Stabiel</span><span class="sxs-lookup"><span data-stu-id="ebd81-143">Stable</span></span> |<span data-ttu-id="ebd81-144">meest recente</span><span class="sxs-lookup"><span data-stu-id="ebd81-144">latest</span></span> |<span data-ttu-id="ebd81-145">Ja</span><span class="sxs-lookup"><span data-stu-id="ebd81-145">yes</span></span> |
| <span data-ttu-id="ebd81-146">Debian</span><span class="sxs-lookup"><span data-stu-id="ebd81-146">Debian</span></span> |<span data-ttu-id="ebd81-147">credativ</span><span class="sxs-lookup"><span data-stu-id="ebd81-147">credativ</span></span> |<span data-ttu-id="ebd81-148">Debian</span><span class="sxs-lookup"><span data-stu-id="ebd81-148">Debian</span></span> |<span data-ttu-id="ebd81-149">8</span><span class="sxs-lookup"><span data-stu-id="ebd81-149">8</span></span> |<span data-ttu-id="ebd81-150">meest recente</span><span class="sxs-lookup"><span data-stu-id="ebd81-150">latest</span></span> |<span data-ttu-id="ebd81-151">Er is geen</span><span class="sxs-lookup"><span data-stu-id="ebd81-151">no</span></span> |
| <span data-ttu-id="ebd81-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ebd81-152">openSUSE</span></span> |<span data-ttu-id="ebd81-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="ebd81-153">SUSE</span></span> |<span data-ttu-id="ebd81-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ebd81-154">openSUSE</span></span> |<span data-ttu-id="ebd81-155">13.2</span><span class="sxs-lookup"><span data-stu-id="ebd81-155">13.2</span></span> |<span data-ttu-id="ebd81-156">meest recente</span><span class="sxs-lookup"><span data-stu-id="ebd81-156">latest</span></span> |<span data-ttu-id="ebd81-157">Er is geen</span><span class="sxs-lookup"><span data-stu-id="ebd81-157">no</span></span> |
| <span data-ttu-id="ebd81-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="ebd81-158">RHEL</span></span> |<span data-ttu-id="ebd81-159">RedHat</span><span class="sxs-lookup"><span data-stu-id="ebd81-159">Redhat</span></span> |<span data-ttu-id="ebd81-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="ebd81-160">RHEL</span></span> |<span data-ttu-id="ebd81-161">7.2</span><span class="sxs-lookup"><span data-stu-id="ebd81-161">7.2</span></span> |<span data-ttu-id="ebd81-162">meest recente</span><span class="sxs-lookup"><span data-stu-id="ebd81-162">latest</span></span> |<span data-ttu-id="ebd81-163">Er is geen</span><span class="sxs-lookup"><span data-stu-id="ebd81-163">no</span></span> |
| <span data-ttu-id="ebd81-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="ebd81-164">UbuntuLTS</span></span> |<span data-ttu-id="ebd81-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="ebd81-165">Canonical</span></span> |<span data-ttu-id="ebd81-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="ebd81-166">UbuntuServer</span></span> |<span data-ttu-id="ebd81-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="ebd81-167">14.04.4-LTS</span></span> |<span data-ttu-id="ebd81-168">meest recente</span><span class="sxs-lookup"><span data-stu-id="ebd81-168">latest</span></span> |<span data-ttu-id="ebd81-169">Ja</span><span class="sxs-lookup"><span data-stu-id="ebd81-169">yes</span></span> |

<span data-ttu-id="ebd81-170">We kunnen werken met onze partners tooget cloud-init opgenomen en werken in dat ze tooAzure bieden Hallo-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="ebd81-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="ebd81-171">Toevoegen van een cloud-init script toohello maken van VM's met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ebd81-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="ebd81-172">toolaunch een cloud-init-script bij het maken van een virtuele machine in Azure, geef Hallo cloud init-bestand met hello Azure CLI `--custom-data` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="ebd81-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="ebd81-173">Maken van een groep resource toolaunch virtuele machines in met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ebd81-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ebd81-174">Hallo volgende voorbeeld maakt Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ebd81-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ebd81-175">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="ebd81-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="ebd81-176">Maken van een cloud-init script tooset Hallo hostnaam van een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="ebd81-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="ebd81-177">Een van de belangrijkste instellingen voor een Linux-VM en eenvoudigste Hallo zijn Hallo hostnaam.</span><span class="sxs-lookup"><span data-stu-id="ebd81-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="ebd81-178">We kunnen eenvoudig Stel dit met behulp van cloud-init met dit script.</span><span class="sxs-lookup"><span data-stu-id="ebd81-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="ebd81-179">Voorbeeld van de cloud init script met de naam `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="ebd81-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="ebd81-180">Tijdens opstarten Hallo Hallo VM stelt dit script cloud init Hallo hostnaam te*myservername*.</span><span class="sxs-lookup"><span data-stu-id="ebd81-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="ebd81-181">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="ebd81-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="ebd81-182">Aanmelding en controleer of de hostnaam Hallo Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ebd81-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="ebd81-183">Een cloud-init-script maken</span><span class="sxs-lookup"><span data-stu-id="ebd81-183">Create a cloud-init script</span></span>
<span data-ttu-id="ebd81-184">Voor beveiliging moet uw tooupdate Ubuntu VM op Hallo eerst wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="ebd81-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="ebd81-185">Met behulp van cloud-init kunt we doen dat script, afhankelijk van de Linux-distributie Hallo u Hello volgen.</span><span class="sxs-lookup"><span data-stu-id="ebd81-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="ebd81-186">Cloud-init voorbeeldscript `cloud_config_apt_upgrade.txt` voor Hallo Debian-familie</span><span class="sxs-lookup"><span data-stu-id="ebd81-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="ebd81-187">Nadat Linux is opgestart, alle geïnstalleerd hello-pakketten worden bijgewerkt via **apt get-**.</span><span class="sxs-lookup"><span data-stu-id="ebd81-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="ebd81-188">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="ebd81-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="ebd81-189">Aanmelding en controleer of alle pakketten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ebd81-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="ebd81-190">Een cloud-init script tooadd een tooLinux gebruiker maken</span><span class="sxs-lookup"><span data-stu-id="ebd81-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="ebd81-191">Een Hallo eerste taken op een nieuwe Linux-VM is een gebruiker voor uzelf of met behulp van tooavoid tooadd *hoofdmap*.</span><span class="sxs-lookup"><span data-stu-id="ebd81-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="ebd81-192">SSH-sleutels zijn best practice voor beveiliging en bruikbaarheid en ze worden toegevoegd toohello *~/.ssh/authorized_keys* bestand met dit script cloud init.</span><span class="sxs-lookup"><span data-stu-id="ebd81-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="ebd81-193">Cloud-init voorbeeldscript `cloud_config_add_users.txt` voor Debian-familie</span><span class="sxs-lookup"><span data-stu-id="ebd81-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="ebd81-194">Nadat Linux is opgestart, zijn alle gebruikers van de vermelde Hallo gemaakt en toegevoegd toohello sudo-groep.</span><span class="sxs-lookup"><span data-stu-id="ebd81-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="ebd81-195">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init tooconfigure deze tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="ebd81-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="ebd81-196">Aanmelding en verificatie van gebruiker Hallo nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebd81-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="ebd81-197">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="ebd81-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="ebd81-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebd81-198">Next steps</span></span>
<span data-ttu-id="ebd81-199">Cloud-init wordt steeds een standaardmanier toomodify uw Linux VM op opstarten.</span><span class="sxs-lookup"><span data-stu-id="ebd81-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="ebd81-200">Azure heeft bovendien VM-extensies u toomodify kunnen uw LinuxVM op opstarten of terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ebd81-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="ebd81-201">U kunt bijvoorbeeld gebruikersgegevens of hello Azure VMAccessExtension tooreset SSH gebruiken terwijl Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ebd81-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="ebd81-202">Met cloud-init moet u een wachtwoord opnieuw opstarten tooreset Hallo.</span><span class="sxs-lookup"><span data-stu-id="ebd81-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="ebd81-203">Over functies en uitbreidingen van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="ebd81-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="ebd81-204">Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="ebd81-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
