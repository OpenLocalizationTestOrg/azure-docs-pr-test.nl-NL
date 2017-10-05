---
title: Cloud-init gebruiken voor het aanpassen van een Linux-VM | Microsoft Docs
description: Het gebruik van cloud-init voor het aanpassen van een Linux-VM tijdens het maken van met de Azure CLI 2.0
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="a76f9-103">Cloud-init gebruiken voor het aanpassen van een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="a76f9-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="a76f9-104">Dit artikel laat zien hoe u een cloud-init-script voor het instellen van de hostnaam, geïnstalleerde pakketten bijwerken en beheren van gebruikersaccounts met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a76f9-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="a76f9-105">De cloud init-scripts worden aangeroepen wanneer u een virtuele machine (VM) van Azure CLI maken.</span><span class="sxs-lookup"><span data-stu-id="a76f9-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="a76f9-106">Zie voor een meer gedetailleerd overzicht over het installeren van toepassingen, configuratiebestanden schrijven en injecteren sleutels van de Sleutelkluis, [in deze zelfstudie](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a76f9-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="a76f9-107">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a76f9-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="a76f9-108">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="a76f9-108">Quick commands</span></span>
<span data-ttu-id="a76f9-109">Een cloud-init.txt-script dat Hiermee stelt u de hostnaam, updates van alle pakketten en voegt een sudo-gebruiker toe aan Linux maken.</span><span class="sxs-lookup"><span data-stu-id="a76f9-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="a76f9-110">Maak een resourcegroep om te starten van virtuele machines in met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a76f9-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a76f9-111">Het volgende voorbeeld wordt de resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a76f9-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a76f9-112">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten met het `--custom-data` parameter.</span><span class="sxs-lookup"><span data-stu-id="a76f9-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="a76f9-113">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="a76f9-113">Detailed walkthrough</span></span>
<span data-ttu-id="a76f9-114">Wanneer u een nieuwe Linux VM start, kunt u een standaard Linux-VM met niets wel aangepaste of gereed voor uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="a76f9-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="a76f9-115">[Cloud-init](https://cloudinit.readthedocs.org) is een standaard manier om een script of configuratie-instellingen in die Linux VM invoeren als deze voor de eerste keer wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="a76f9-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="a76f9-116">In Azure, er zijn een aantal verschillende manieren te wijzigen naar een Linux-VM als dit wordt geïmplementeerd of opgestart.</span><span class="sxs-lookup"><span data-stu-id="a76f9-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="a76f9-117">Scripts met cloud-init invoeren.</span><span class="sxs-lookup"><span data-stu-id="a76f9-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="a76f9-118">Scripts met de Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a76f9-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="a76f9-119">Een Azure-sjabloon met behulp van cloud-init.</span><span class="sxs-lookup"><span data-stu-id="a76f9-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="a76f9-120">Een Azure-sjabloon met [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="a76f9-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="a76f9-121">Scripts op elk gewenst moment na opstarten invoeren:</span><span class="sxs-lookup"><span data-stu-id="a76f9-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="a76f9-122">SSH opdrachten rechtstreeks uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a76f9-122">SSH to run commands directly</span></span>
* <span data-ttu-id="a76f9-123">Scripts met de Azure injecteren [VMAccess-extensie](using-vmaccess-extension.md), imperatively of in een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a76f9-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="a76f9-124">Configuration management-hulpprogramma's zoals Ansible, Salt of Chef of Puppet.</span><span class="sxs-lookup"><span data-stu-id="a76f9-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="a76f9-125">Een script wordt uitgevoerd als hoofdmap op dezelfde manier via SSH in VMAccess-extensie.</span><span class="sxs-lookup"><span data-stu-id="a76f9-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="a76f9-126">Echter, met behulp van de VM-extensie kan verschillende functies die Azure biedt die nuttig is afhankelijk van uw scenario kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="a76f9-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="a76f9-127">Cloud-init beschikbaarheid op Azure VM snelle invoer installatiekopie aliassen:</span><span class="sxs-lookup"><span data-stu-id="a76f9-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="a76f9-128">Alias</span><span class="sxs-lookup"><span data-stu-id="a76f9-128">Alias</span></span> | <span data-ttu-id="a76f9-129">Uitgever</span><span class="sxs-lookup"><span data-stu-id="a76f9-129">Publisher</span></span> | <span data-ttu-id="a76f9-130">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="a76f9-130">Offer</span></span> | <span data-ttu-id="a76f9-131">SKU</span><span class="sxs-lookup"><span data-stu-id="a76f9-131">SKU</span></span> | <span data-ttu-id="a76f9-132">Versie</span><span class="sxs-lookup"><span data-stu-id="a76f9-132">Version</span></span> | <span data-ttu-id="a76f9-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="a76f9-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="a76f9-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="a76f9-134">CentOS</span></span> |<span data-ttu-id="a76f9-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="a76f9-135">OpenLogic</span></span> |<span data-ttu-id="a76f9-136">Centos</span><span class="sxs-lookup"><span data-stu-id="a76f9-136">Centos</span></span> |<span data-ttu-id="a76f9-137">7.2</span><span class="sxs-lookup"><span data-stu-id="a76f9-137">7.2</span></span> |<span data-ttu-id="a76f9-138">meest recente</span><span class="sxs-lookup"><span data-stu-id="a76f9-138">latest</span></span> |<span data-ttu-id="a76f9-139">Er is geen</span><span class="sxs-lookup"><span data-stu-id="a76f9-139">no</span></span> |
| <span data-ttu-id="a76f9-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a76f9-140">CoreOS</span></span> |<span data-ttu-id="a76f9-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a76f9-141">CoreOS</span></span> |<span data-ttu-id="a76f9-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a76f9-142">CoreOS</span></span> |<span data-ttu-id="a76f9-143">Stabiel</span><span class="sxs-lookup"><span data-stu-id="a76f9-143">Stable</span></span> |<span data-ttu-id="a76f9-144">meest recente</span><span class="sxs-lookup"><span data-stu-id="a76f9-144">latest</span></span> |<span data-ttu-id="a76f9-145">Ja</span><span class="sxs-lookup"><span data-stu-id="a76f9-145">yes</span></span> |
| <span data-ttu-id="a76f9-146">Debian</span><span class="sxs-lookup"><span data-stu-id="a76f9-146">Debian</span></span> |<span data-ttu-id="a76f9-147">credativ</span><span class="sxs-lookup"><span data-stu-id="a76f9-147">credativ</span></span> |<span data-ttu-id="a76f9-148">Debian</span><span class="sxs-lookup"><span data-stu-id="a76f9-148">Debian</span></span> |<span data-ttu-id="a76f9-149">8</span><span class="sxs-lookup"><span data-stu-id="a76f9-149">8</span></span> |<span data-ttu-id="a76f9-150">meest recente</span><span class="sxs-lookup"><span data-stu-id="a76f9-150">latest</span></span> |<span data-ttu-id="a76f9-151">Er is geen</span><span class="sxs-lookup"><span data-stu-id="a76f9-151">no</span></span> |
| <span data-ttu-id="a76f9-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="a76f9-152">openSUSE</span></span> |<span data-ttu-id="a76f9-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="a76f9-153">SUSE</span></span> |<span data-ttu-id="a76f9-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="a76f9-154">openSUSE</span></span> |<span data-ttu-id="a76f9-155">13.2</span><span class="sxs-lookup"><span data-stu-id="a76f9-155">13.2</span></span> |<span data-ttu-id="a76f9-156">meest recente</span><span class="sxs-lookup"><span data-stu-id="a76f9-156">latest</span></span> |<span data-ttu-id="a76f9-157">Er is geen</span><span class="sxs-lookup"><span data-stu-id="a76f9-157">no</span></span> |
| <span data-ttu-id="a76f9-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="a76f9-158">RHEL</span></span> |<span data-ttu-id="a76f9-159">RedHat</span><span class="sxs-lookup"><span data-stu-id="a76f9-159">Redhat</span></span> |<span data-ttu-id="a76f9-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="a76f9-160">RHEL</span></span> |<span data-ttu-id="a76f9-161">7.2</span><span class="sxs-lookup"><span data-stu-id="a76f9-161">7.2</span></span> |<span data-ttu-id="a76f9-162">meest recente</span><span class="sxs-lookup"><span data-stu-id="a76f9-162">latest</span></span> |<span data-ttu-id="a76f9-163">Er is geen</span><span class="sxs-lookup"><span data-stu-id="a76f9-163">no</span></span> |
| <span data-ttu-id="a76f9-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="a76f9-164">UbuntuLTS</span></span> |<span data-ttu-id="a76f9-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="a76f9-165">Canonical</span></span> |<span data-ttu-id="a76f9-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="a76f9-166">UbuntuServer</span></span> |<span data-ttu-id="a76f9-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="a76f9-167">14.04.4-LTS</span></span> |<span data-ttu-id="a76f9-168">meest recente</span><span class="sxs-lookup"><span data-stu-id="a76f9-168">latest</span></span> |<span data-ttu-id="a76f9-169">Ja</span><span class="sxs-lookup"><span data-stu-id="a76f9-169">yes</span></span> |

<span data-ttu-id="a76f9-170">We werken met onze partners ophalen van cloud-init opgenomen en in de afbeeldingen die ze naar Azure bieden werkt.</span><span class="sxs-lookup"><span data-stu-id="a76f9-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="a76f9-171">Een cloud-init-script toevoegen aan de virtuele machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a76f9-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="a76f9-172">Als u wilt een cloud-init-script wordt gestart bij het maken van een virtuele machine in Azure, geeft u het cloud-init-bestand met de Azure CLI `--custom-data` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="a76f9-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="a76f9-173">Maak een resourcegroep om te starten van virtuele machines in met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a76f9-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a76f9-174">Het volgende voorbeeld wordt de resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a76f9-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a76f9-175">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.</span><span class="sxs-lookup"><span data-stu-id="a76f9-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="a76f9-176">Een cloud-init-script voor het instellen van de hostnaam van een Linux-VM maken</span><span class="sxs-lookup"><span data-stu-id="a76f9-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="a76f9-177">Een van de eenvoudigste en meest belangrijke instellingen voor een Linux-VM is de hostnaam.</span><span class="sxs-lookup"><span data-stu-id="a76f9-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="a76f9-178">We kunnen eenvoudig Stel dit met behulp van cloud-init met dit script.</span><span class="sxs-lookup"><span data-stu-id="a76f9-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="a76f9-179">Voorbeeld van de cloud init script met de naam `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="a76f9-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="a76f9-180">Dit script cloud init wordt tijdens het opstarten van de virtuele machine, de hostnaam ingesteld op *myservername*.</span><span class="sxs-lookup"><span data-stu-id="a76f9-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="a76f9-181">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.</span><span class="sxs-lookup"><span data-stu-id="a76f9-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="a76f9-182">Aanmelding en controleer of de hostnaam van de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a76f9-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="a76f9-183">Een cloud-init-script maken</span><span class="sxs-lookup"><span data-stu-id="a76f9-183">Create a cloud-init script</span></span>
<span data-ttu-id="a76f9-184">Voor beveiliging moet uw Ubuntu VM bijwerken voor het eerst wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="a76f9-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="a76f9-185">Met behulp van cloud-init die we doen dat met het script volgen, afhankelijk van de Linux-distributie die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a76f9-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="a76f9-186">Cloud-init voorbeeldscript `cloud_config_apt_upgrade.txt` voor de Debian-familie</span><span class="sxs-lookup"><span data-stu-id="a76f9-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="a76f9-187">Nadat Linux is opgestart, de geïnstalleerde pakketten worden bijgewerkt via **apt get-**.</span><span class="sxs-lookup"><span data-stu-id="a76f9-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="a76f9-188">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.</span><span class="sxs-lookup"><span data-stu-id="a76f9-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="a76f9-189">Aanmelding en controleer of alle pakketten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a76f9-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="a76f9-190">Een cloud-init script een gebruiker toevoegen aan Linux maken</span><span class="sxs-lookup"><span data-stu-id="a76f9-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="a76f9-191">Een van de eerste taken op een nieuwe Linux-VM is een gebruiker toevoegen voor uzelf of te vermijden met behulp van *hoofdmap*.</span><span class="sxs-lookup"><span data-stu-id="a76f9-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="a76f9-192">SSH-sleutels zijn best practice voor beveiliging en bruikbaarheid en ze worden toegevoegd aan de *~/.ssh/authorized_keys* bestand met dit script cloud init.</span><span class="sxs-lookup"><span data-stu-id="a76f9-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="a76f9-193">Cloud-init voorbeeldscript `cloud_config_add_users.txt` voor Debian-familie</span><span class="sxs-lookup"><span data-stu-id="a76f9-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="a76f9-194">Nadat Linux is opgestart, worden alle vermelde gebruikers gemaakt en toegevoegd aan de sudo-groep.</span><span class="sxs-lookup"><span data-stu-id="a76f9-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="a76f9-195">Maak een Linux-VM met [az vm maken](/cli/azure/vm#create) met behulp van cloud-init te configureren tijdens opstarten.</span><span class="sxs-lookup"><span data-stu-id="a76f9-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="a76f9-196">Aanmelding en controleer of de nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a76f9-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="a76f9-197">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="a76f9-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="a76f9-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a76f9-198">Next steps</span></span>
<span data-ttu-id="a76f9-199">Cloud-init steeds één standaardmethode voor het wijzigen van uw Linux VM op opstarten.</span><span class="sxs-lookup"><span data-stu-id="a76f9-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="a76f9-200">Azure heeft ook een VM-extensies wijzigen van uw LinuxVM op opstarten of kunnen terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a76f9-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="a76f9-201">Bijvoorbeeld, kunt u de Azure-VMAccessExtension opnieuw instellen van SSH of gebruikersgegevens terwijl de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a76f9-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="a76f9-202">Met cloud-init moet u opnieuw het wachtwoord opnieuw wilt opstarten.</span><span class="sxs-lookup"><span data-stu-id="a76f9-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="a76f9-203">Over functies en uitbreidingen van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a76f9-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="a76f9-204">Beheren van gebruikers, SSH en controleer of het herstellen van schijven op Azure Linux VM's met behulp van de VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="a76f9-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)