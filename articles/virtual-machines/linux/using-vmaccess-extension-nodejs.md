---
title: aaaReset toegang over het gebruik van Azure Linux VM's Hallo VMAccess-extensie | Microsoft Docs
description: Opnieuw instellen op Azure Linux VM's met behulp van Hallo VMAccess-extensie.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="9d769-103">Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van VMAccess-extensie Hallo Hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9d769-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="9d769-104">Dit artikel ziet u hoe toouse hello Azure VMAcesss extensie toocheck of herstellen van een schijf, gebruikerstoegang opnieuw instellen, beheren van gebruikersaccounts of opnieuw Hallo SSHD configureren op Linux.</span><span class="sxs-lookup"><span data-stu-id="9d769-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="9d769-105">Hallo artikel is vereist:</span><span class="sxs-lookup"><span data-stu-id="9d769-105">hello article requires:</span></span>

* <span data-ttu-id="9d769-106">een Azure-account ([probeer een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="9d769-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="9d769-107">Hallo [Azure CLI](../../cli-install-nodejs.md) aangemeld `azure login`.</span><span class="sxs-lookup"><span data-stu-id="9d769-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="9d769-108">Hello Azure CLI *moet* modus Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="9d769-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9d769-109">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="9d769-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="9d769-110">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9d769-111">[Azure CLI 1.0](#quick-commands)– onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="9d769-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9d769-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="9d769-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="9d769-113">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="9d769-113">Quick commands</span></span>
<span data-ttu-id="9d769-114">Er zijn twee manieren toouse VMAccess op uw virtuele Linux-machines:</span><span class="sxs-lookup"><span data-stu-id="9d769-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="9d769-115">Met behulp van hello Azure CLI 1.0 en Hallo vereiste parameters.</span><span class="sxs-lookup"><span data-stu-id="9d769-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="9d769-116">Met behulp van onbewerkte JSON-bestanden die VMAccess verwerkt en klik vervolgens op te volgen.</span><span class="sxs-lookup"><span data-stu-id="9d769-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="9d769-117">Voor Hallo snelle opdracht sectie, gaan we toouse hello Azure CLI 1.0 `azure vm reset-access` methode.</span><span class="sxs-lookup"><span data-stu-id="9d769-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="9d769-118">Volgende opdrachtvoorbeelden Vervang in Hallo Hallo waarden met "voorbeeld" hello waarden van uw eigen omgeving.</span><span class="sxs-lookup"><span data-stu-id="9d769-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="9d769-119">Een resourcegroep en een virtuele Linux-machine maken</span><span class="sxs-lookup"><span data-stu-id="9d769-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="9d769-120">Een Debian virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="9d769-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="9d769-121">Root-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="9d769-121">Reset root password</span></span>
<span data-ttu-id="9d769-122">tooreset hello root-wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="9d769-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="9d769-123">SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="9d769-123">SSH key reset</span></span>
<span data-ttu-id="9d769-124">tooreset hello SSH-sleutel van een gebruiker niet hoofdmap:</span><span class="sxs-lookup"><span data-stu-id="9d769-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="9d769-125">Een gebruiker maken</span><span class="sxs-lookup"><span data-stu-id="9d769-125">Create a user</span></span>
<span data-ttu-id="9d769-126">een gebruiker toocreate:</span><span class="sxs-lookup"><span data-stu-id="9d769-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="9d769-127">Een gebruiker verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d769-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="9d769-128">SSHD opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="9d769-128">Reset SSHD</span></span>
<span data-ttu-id="9d769-129">tooreset hello SSHD configuratie:</span><span class="sxs-lookup"><span data-stu-id="9d769-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="9d769-130">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="9d769-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="9d769-131">VMAccess gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="9d769-131">VMAccess defined:</span></span>
<span data-ttu-id="9d769-132">Hallo-schijf op uw Linux-VM worden fouten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9d769-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="9d769-133">U enigszins Hallo hoofdwachtwoord voor uw Linux-VM opnieuw instellen of uw persoonlijke SSH-sleutel per ongeluk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9d769-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="9d769-134">Als dat is gebeurd terug in Hallo dagen van Hallo datacenter, zou u moet er toodrive en open vervolgens Hallo KVM tooget op Hallo server-console.</span><span class="sxs-lookup"><span data-stu-id="9d769-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="9d769-135">Hello Azure VMAccess-extensie beschouwen als die KVM-switch waarmee u tooaccess console tooreset toegang tooLinux Hallo of voer schijfonderhoud niveau.</span><span class="sxs-lookup"><span data-stu-id="9d769-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="9d769-136">Voor Hallo gedetailleerde uitleg gaan we toouse Hallo lange vorm van VMAccess dat gebruikmaakt van onbewerkte JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="9d769-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="9d769-137">Deze VMAccess JSON-bestanden kunnen ook worden aangeroepen vanuit de Azure-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9d769-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="9d769-138">Het gebruik van VMAccess toocheck of reparatie van de Hallo schijf van een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="9d769-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="9d769-139">U vmaccess gebruikt kunt u een fsck doen uitvoeren op de schijf Hallo onder uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="9d769-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="9d769-140">U kunt ook een schijf controleren en de herstellen van een schijf met behulp van een VMAccess doen.</span><span class="sxs-lookup"><span data-stu-id="9d769-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="9d769-141">Gebruik dit script VMAccess toocheck en herstel Hallo schijf:</span><span class="sxs-lookup"><span data-stu-id="9d769-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="9d769-142">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="9d769-143">Met behulp van VMAccess tooreset gebruiker toegang tooLinux</span><span class="sxs-lookup"><span data-stu-id="9d769-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="9d769-144">Als u toegang tooroot kwijt op uw Linux-VM bent hebt, kunt u een hoofdwachtwoord VMAccess script tooreset Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="9d769-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="9d769-145">tooreset hello hoofdwachtwoord, gebruik dit script vmaccess gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9d769-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="9d769-146">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="9d769-147">tooreset hello SSH-sleutel van een niet-hoofdgebruiker dit script VMAccess gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d769-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="9d769-148">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="9d769-149">Met behulp van VMAccess toomanage gebruikersaccounts op Linux</span><span class="sxs-lookup"><span data-stu-id="9d769-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="9d769-150">VMAccess is een pythonscript dat gebruikt toomanage gebruikers op uw Linux-VM worden kan zonder aanmelden en het gebruik van sudo of Hallo root-account.</span><span class="sxs-lookup"><span data-stu-id="9d769-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="9d769-151">toocreate een gebruiker, gebruikt u dit script vmaccess gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9d769-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="9d769-152">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="9d769-153">toodelete een gebruiker, gebruikt u dit script vmaccess gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9d769-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="9d769-154">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="9d769-155">Met behulp van VMAccess tooreset hello SSHD configuratie</span><span class="sxs-lookup"><span data-stu-id="9d769-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="9d769-156">Als u wijzigingen toohello Linux VM's SSHD configuratie en SSH-verbinding sluiten Hallo voordat verifiëren, Hallo wijzigingen aanbrengt, u kan worden voorkomen dat SSH'ing weer in.</span><span class="sxs-lookup"><span data-stu-id="9d769-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="9d769-157">VMAccess mag gebruikte tooreset hello SSHD configuratie back tooa bekende juiste configuratie zonder worden geregistreerd in via SSH.</span><span class="sxs-lookup"><span data-stu-id="9d769-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="9d769-158">tooreset hello SSHD configuratie dit script VMAccess gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d769-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="9d769-159">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d769-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="9d769-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d769-160">Next steps</span></span>
<span data-ttu-id="9d769-161">Bijwerken van Linux, met behulp van Azure VMAccess extensies één methode toomake wijzigingen op een actieve Linux VM is.</span><span class="sxs-lookup"><span data-stu-id="9d769-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="9d769-162">U kunt ook hulpprogramma's zoals cloud init en Azure-sjablonen toomodify uw Linux-VM gebruiken bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="9d769-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="9d769-163">Over functies en uitbreidingen van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9d769-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="9d769-164">Azure Resource Manager-sjablonen met Linux VM-extensies</span><span class="sxs-lookup"><span data-stu-id="9d769-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="9d769-165">Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="9d769-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

